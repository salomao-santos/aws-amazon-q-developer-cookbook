# Input Validation Recipe

## Description
Implement robust input validation and sanitization to prevent injection attacks and data corruption.

## Prompt Template

```
Add input validation and sanitization to the following [LANGUAGE] code:

[PASTE_CODE]

Security requirements:
- Validate all user inputs
- Sanitize inputs to prevent [XSS/SQL injection/Command injection]
- Add type checking and format validation
- Implement allowlist validation where possible
- Add length limits
- Validate against schemas/patterns
- Return clear validation error messages
- Follow [FRAMEWORK] security best practices
- Use established validation libraries
```

## Example Usage

### Example 1: API Input Validation

**Prompt:**
```
Add input validation and sanitization to the following Express.js code:

app.post('/api/users/search', (req, res) => {
  const { query, limit, offset } = req.body;
  
  const sql = `SELECT * FROM users WHERE name LIKE '%${query}%' LIMIT ${limit} OFFSET ${offset}`;
  db.query(sql, (err, results) => {
    if (err) return res.status(500).json({ error: 'Database error' });
    res.json(results);
  });
});

Security requirements:
- Validate all user inputs (query, limit, offset)
- Sanitize inputs to prevent SQL injection
- Add type checking (query: string, limit/offset: numbers)
- Implement allowlist validation for LIMIT and OFFSET
- Add length limits for query (max 100 characters)
- Use parameterized queries instead of string concatenation
- Return clear validation error messages
- Follow Express.js security best practices
- Use express-validator library
```

**Expected Output:**
```javascript
const { body, validationResult } = require('express-validator');

app.post('/api/users/search',
  // Validation middleware
  [
    body('query')
      .isString()
      .trim()
      .isLength({ min: 1, max: 100 })
      .withMessage('Query must be 1-100 characters')
      .escape(), // Sanitize for XSS prevention
    
    body('limit')
      .optional()
      .isInt({ min: 1, max: 100 })
      .withMessage('Limit must be between 1 and 100')
      .toInt(),
    
    body('offset')
      .optional()
      .isInt({ min: 0 })
      .withMessage('Offset must be non-negative')
      .toInt()
  ],
  async (req, res) => {
    // Check validation results
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
      return res.status(400).json({ 
        error: 'Validation failed',
        details: errors.array()
      });
    }
    
    const { query, limit = 10, offset = 0 } = req.body;
    
    // Use parameterized query to prevent SQL injection
    const sql = 'SELECT id, name, email FROM users WHERE name LIKE ? LIMIT ? OFFSET ?';
    const params = [`%${query}%`, limit, offset];
    
    try {
      const results = await db.query(sql, params);
      res.json(results);
    } catch (err) {
      console.error('Database error:', err);
      res.status(500).json({ error: 'Internal server error' });
    }
  }
);
```

### Example 2: Form Input Validation (React)

**Prompt:**
```
Add input validation to the following React registration form:

function RegistrationForm() {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  
  const handleSubmit = (e) => {
    e.preventDefault();
    fetch('/api/register', {
      method: 'POST',
      body: JSON.stringify({ email, password })
    });
  };
  
  return (
    <form onSubmit={handleSubmit}>
      <input value={email} onChange={(e) => setEmail(e.target.value)} />
      <input type="password" value={password} onChange={(e) => setPassword(e.target.value)} />
      <button>Register</button>
    </form>
  );
}

Security requirements:
- Validate email format (RFC 5322)
- Validate password strength (min 8 chars, uppercase, lowercase, number, special char)
- Add real-time validation feedback
- Sanitize inputs before display
- Prevent form submission with invalid data
- Display clear error messages
- Use a validation library (Yup or Zod)
- Follow React security best practices
```

**Expected Output:**
```javascript
import { useState } from 'react';
import * as Yup from 'yup';

const registrationSchema = Yup.object().shape({
  email: Yup.string()
    .email('Invalid email address')
    .required('Email is required')
    .max(255, 'Email too long'),
  
  password: Yup.string()
    .required('Password is required')
    .min(8, 'Password must be at least 8 characters')
    .max(128, 'Password too long')
    .matches(
      /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]/,
      'Password must contain uppercase, lowercase, number, and special character'
    )
});

function RegistrationForm() {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [errors, setErrors] = useState({});
  const [isSubmitting, setIsSubmitting] = useState(false);
  
  const validateField = async (field, value) => {
    try {
      await registrationSchema.validateAt(field, { [field]: value });
      setErrors(prev => ({ ...prev, [field]: null }));
    } catch (err) {
      setErrors(prev => ({ ...prev, [field]: err.message }));
    }
  };
  
  const handleEmailChange = (e) => {
    const value = e.target.value;
    setEmail(value);
    validateField('email', value);
  };
  
  const handlePasswordChange = (e) => {
    const value = e.target.value;
    setPassword(value);
    validateField('password', value);
  };
  
  const handleSubmit = async (e) => {
    e.preventDefault();
    
    try {
      // Validate entire form
      await registrationSchema.validate(
        { email, password },
        { abortEarly: false }
      );
      
      setIsSubmitting(true);
      
      const response = await fetch('/api/register', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({ email, password })
      });
      
      if (!response.ok) {
        throw new Error('Registration failed');
      }
      
      // Handle success
      const data = await response.json();
      console.log('Registration successful:', data);
      
    } catch (err) {
      if (err.inner) {
        // Yup validation errors
        const validationErrors = {};
        err.inner.forEach(error => {
          validationErrors[error.path] = error.message;
        });
        setErrors(validationErrors);
      } else {
        // Server error
        console.error('Registration error:', err);
        setErrors({ submit: 'Registration failed. Please try again.' });
      }
    } finally {
      setIsSubmitting(false);
    }
  };
  
  const hasErrors = Object.values(errors).some(error => error !== null);
  
  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label htmlFor="email">Email</label>
        <input
          id="email"
          type="email"
          value={email}
          onChange={handleEmailChange}
          aria-invalid={!!errors.email}
          aria-describedby={errors.email ? "email-error" : undefined}
        />
        {errors.email && (
          <span id="email-error" role="alert" style={{ color: 'red' }}>
            {errors.email}
          </span>
        )}
      </div>
      
      <div>
        <label htmlFor="password">Password</label>
        <input
          id="password"
          type="password"
          value={password}
          onChange={handlePasswordChange}
          aria-invalid={!!errors.password}
          aria-describedby={errors.password ? "password-error" : undefined}
        />
        {errors.password && (
          <span id="password-error" role="alert" style={{ color: 'red' }}>
            {errors.password}
          </span>
        )}
      </div>
      
      {errors.submit && (
        <div role="alert" style={{ color: 'red' }}>
          {errors.submit}
        </div>
      )}
      
      <button 
        type="submit" 
        disabled={isSubmitting || hasErrors || !email || !password}
      >
        {isSubmitting ? 'Registering...' : 'Register'}
      </button>
    </form>
  );
}

export default RegistrationForm;
```

### Example 3: Python Input Validation

**Prompt:**
```
Add input validation to the following Python FastAPI endpoint:

@app.post("/products")
async def create_product(name: str, price: float, category: str):
    product = {
        "name": name,
        "price": price,
        "category": category
    }
    await db.products.insert_one(product)
    return product

Security requirements:
- Validate all inputs using Pydantic models
- Sanitize name and category (max length, allowed characters)
- Validate price (positive number, max 2 decimal places)
- Add field constraints (required, optional)
- Return validation error messages
- Follow FastAPI security best practices
```

**Expected Output:**
```python
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel, Field, validator
from typing import Optional
import re

app = FastAPI()

class ProductCreate(BaseModel):
    """Product creation model with validation"""
    
    name: str = Field(
        ...,
        min_length=1,
        max_length=200,
        description="Product name"
    )
    price: float = Field(
        ...,
        gt=0,
        le=999999.99,
        description="Product price in USD"
    )
    category: str = Field(
        ...,
        min_length=1,
        max_length=50,
        description="Product category"
    )
    description: Optional[str] = Field(
        None,
        max_length=1000,
        description="Optional product description"
    )
    
    @validator('name')
    def validate_name(cls, v):
        """Validate name contains only allowed characters"""
        # Allow letters, numbers, spaces, hyphens, and common punctuation
        if not re.match(r'^[a-zA-Z0-9\s\-.,&()]+$', v):
            raise ValueError(
                'Name can only contain letters, numbers, spaces, and basic punctuation'
            )
        # Trim and normalize whitespace
        return ' '.join(v.split())
    
    @validator('price')
    def validate_price(cls, v):
        """Validate price has max 2 decimal places"""
        if round(v, 2) != v:
            raise ValueError('Price can have at most 2 decimal places')
        return round(v, 2)
    
    @validator('category')
    def validate_category(cls, v):
        """Validate category is from allowed list"""
        allowed_categories = {
            'electronics', 'clothing', 'food', 'books', 
            'toys', 'home', 'sports', 'beauty'
        }
        category_lower = v.lower().strip()
        if category_lower not in allowed_categories:
            raise ValueError(
                f'Category must be one of: {", ".join(allowed_categories)}'
            )
        return category_lower
    
    @validator('description')
    def validate_description(cls, v):
        """Sanitize description if provided"""
        if v is None:
            return v
        # Remove potential XSS characters
        sanitized = re.sub(r'[<>]', '', v)
        return ' '.join(sanitized.split())
    
    class Config:
        schema_extra = {
            "example": {
                "name": "Wireless Mouse",
                "price": 29.99,
                "category": "electronics",
                "description": "Ergonomic wireless mouse with USB receiver"
            }
        }

@app.post("/products", response_model=dict, status_code=201)
async def create_product(product: ProductCreate):
    """
    Create a new product with validated inputs.
    
    Raises:
        HTTPException: If database operation fails
    """
    try:
        # Convert to dict for database insertion
        product_dict = product.dict()
        
        # Insert into database
        result = await db.products.insert_one(product_dict)
        
        # Return created product with ID
        product_dict['id'] = str(result.inserted_id)
        return product_dict
        
    except Exception as e:
        # Log error (don't expose internal details to user)
        print(f"Database error: {e}")
        raise HTTPException(
            status_code=500,
            detail="Failed to create product"
        )
```

## Best Practices

1. **Validate Everything**: Never trust user input
2. **Allowlists Over Denylists**: Define what's allowed, not what's forbidden
3. **Type Checking**: Enforce correct data types
4. **Length Limits**: Prevent buffer overflow and DOS attacks
5. **Format Validation**: Use regex patterns for structured data
6. **Sanitization**: Remove or escape dangerous characters
7. **Schema Validation**: Use libraries like Joi, Yup, Pydantic
8. **Clear Errors**: Provide helpful validation messages

## Common Validation Rules

- **Email**: RFC 5322 format, max length
- **Password**: Min length, complexity requirements
- **URLs**: Valid format, allowed protocols
- **Numbers**: Range, decimal places
- **Dates**: Valid format, reasonable range
- **File Uploads**: Type, size, name validation

## Related Recipes

- [SQL Injection Prevention](./sql-injection.md)
- [XSS Prevention](./xss-prevention.md)
- [API Security](./api-security.md)
