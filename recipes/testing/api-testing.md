# API Testing Recipe

## Description
Generate comprehensive API tests including endpoint testing, validation, error handling, and integration scenarios.

## Prompt Template

```
Create API tests for the following [FRAMEWORK] endpoint using [TEST_FRAMEWORK]:

[PASTE_CODE_OR_ENDPOINT_SPEC]

Requirements:
- Test framework: [Supertest/pytest/RestAssured/etc.]
- Test successful requests (2xx responses)
- Test validation errors (400 responses)
- Test authentication/authorization (401, 403)
- Test not found scenarios (404)
- Test server errors (500)
- Include request/response examples
- Mock database/external services
- Test rate limiting (if applicable)
- Follow REST/GraphQL testing best practices
```

## Example Usage

### Example 1: REST API Endpoint Testing

**Prompt:**
```
Create API tests for the following Express.js endpoint using Supertest and Jest:

router.post('/api/v1/users', async (req, res) => {
  try {
    const { email, firstName, lastName, password } = req.body;
    
    // Validation
    if (!email || !password) {
      return res.status(400).json({ error: 'Email and password required' });
    }
    
    // Check if user exists
    const existing = await User.findOne({ email });
    if (existing) {
      return res.status(409).json({ error: 'User already exists' });
    }
    
    // Create user
    const user = await User.create({ email, firstName, lastName, password });
    
    res.status(201).json({
      id: user.id,
      email: user.email,
      firstName: user.firstName,
      lastName: user.lastName
    });
  } catch (error) {
    res.status(500).json({ error: 'Internal server error' });
  }
});

Requirements:
- Test framework: Supertest with Jest
- Test successful user creation (201)
- Test missing required fields (400)
- Test duplicate email (409)
- Test invalid email format (400)
- Test server errors (500)
- Mock User model methods
- Verify response structure
- Follow REST testing best practices
```

**Expected Output:**
```javascript
const request = require('supertest');
const app = require('../app');
const User = require('../models/User');

// Mock the User model
jest.mock('../models/User');

describe('POST /api/v1/users', () => {
  beforeEach(() => {
    jest.clearAllMocks();
  });
  
  describe('successful user creation', () => {
    test('should create user and return 201 with user data', async () => {
      const newUser = {
        email: 'test@example.com',
        firstName: 'John',
        lastName: 'Doe',
        password: 'SecurePass123!'
      };
      
      const createdUser = {
        id: 1,
        email: 'test@example.com',
        firstName: 'John',
        lastName: 'Doe'
      };
      
      User.findOne.mockResolvedValue(null);
      User.create.mockResolvedValue({ ...createdUser, password: 'hashed' });
      
      const response = await request(app)
        .post('/api/v1/users')
        .send(newUser)
        .expect(201)
        .expect('Content-Type', /json/);
      
      expect(response.body).toEqual(createdUser);
      expect(response.body).not.toHaveProperty('password');
      expect(User.findOne).toHaveBeenCalledWith({ email: newUser.email });
      expect(User.create).toHaveBeenCalledWith(newUser);
    });
    
    test('should create user with only required fields', async () => {
      const minimalUser = {
        email: 'minimal@example.com',
        password: 'SecurePass123!'
      };
      
      User.findOne.mockResolvedValue(null);
      User.create.mockResolvedValue({ 
        id: 2, 
        email: minimalUser.email,
        firstName: null,
        lastName: null
      });
      
      const response = await request(app)
        .post('/api/v1/users')
        .send(minimalUser)
        .expect(201);
      
      expect(response.body.email).toBe(minimalUser.email);
    });
  });
  
  describe('validation errors', () => {
    test('should return 400 when email is missing', async () => {
      const response = await request(app)
        .post('/api/v1/users')
        .send({ password: 'SecurePass123!' })
        .expect(400);
      
      expect(response.body).toHaveProperty('error');
      expect(response.body.error).toMatch(/email.*required/i);
    });
    
    test('should return 400 when password is missing', async () => {
      const response = await request(app)
        .post('/api/v1/users')
        .send({ email: 'test@example.com' })
        .expect(400);
      
      expect(response.body).toHaveProperty('error');
      expect(response.body.error).toMatch(/password.*required/i);
    });
    
    test('should return 400 when both email and password are missing', async () => {
      const response = await request(app)
        .post('/api/v1/users')
        .send({})
        .expect(400);
      
      expect(response.body.error).toMatch(/email.*password.*required/i);
    });
  });
  
  describe('duplicate user scenarios', () => {
    test('should return 409 when user already exists', async () => {
      const existingUser = {
        email: 'existing@example.com',
        password: 'SecurePass123!'
      };
      
      User.findOne.mockResolvedValue({ 
        id: 1, 
        email: existingUser.email 
      });
      
      const response = await request(app)
        .post('/api/v1/users')
        .send(existingUser)
        .expect(409);
      
      expect(response.body.error).toMatch(/already exists/i);
      expect(User.create).not.toHaveBeenCalled();
    });
  });
  
  describe('server errors', () => {
    test('should return 500 when database create fails', async () => {
      User.findOne.mockResolvedValue(null);
      User.create.mockRejectedValue(new Error('Database error'));
      
      const response = await request(app)
        .post('/api/v1/users')
        .send({
          email: 'test@example.com',
          password: 'SecurePass123!'
        })
        .expect(500);
      
      expect(response.body.error).toMatch(/internal server error/i);
    });
    
    test('should return 500 when database find fails', async () => {
      User.findOne.mockRejectedValue(new Error('Database connection error'));
      
      const response = await request(app)
        .post('/api/v1/users')
        .send({
          email: 'test@example.com',
          password: 'SecurePass123!'
        })
        .expect(500);
      
      expect(response.body.error).toMatch(/internal server error/i);
    });
  });
  
  describe('request format validation', () => {
    test('should handle empty request body', async () => {
      const response = await request(app)
        .post('/api/v1/users')
        .send()
        .expect(400);
      
      expect(response.body).toHaveProperty('error');
    });
    
    test('should accept JSON content type', async () => {
      User.findOne.mockResolvedValue(null);
      User.create.mockResolvedValue({ 
        id: 1, 
        email: 'test@example.com' 
      });
      
      await request(app)
        .post('/api/v1/users')
        .set('Content-Type', 'application/json')
        .send(JSON.stringify({
          email: 'test@example.com',
          password: 'SecurePass123!'
        }))
        .expect(201);
    });
  });
});
```

### Example 2: GraphQL API Testing

**Prompt:**
```
Create API tests for the following GraphQL mutation using Apollo Server Testing:

mutation CreateProduct($input: CreateProductInput!) {
  createProduct(input: $input) {
    id
    name
    price
    category {
      id
      name
    }
  }
}

type CreateProductInput {
  name: String!
  description: String
  price: Float!
  categoryId: ID!
}

Requirements:
- Test framework: Apollo Server Testing with Jest
- Test successful product creation
- Test validation errors (missing required fields, invalid price)
- Test invalid category ID (not found)
- Test server errors
- Mock data sources
- Verify nested category response
- Follow GraphQL testing best practices
```

## Best Practices

1. **Comprehensive Coverage**: Test all status codes and scenarios
2. **Mock Dependencies**: Mock databases and external services
3. **Assert Response Structure**: Verify response schema and data types
4. **Test Headers**: Check content-type, authentication headers
5. **Use Factories**: Create reusable test data factories
6. **Test Edge Cases**: Empty bodies, malformed JSON, extra fields
7. **Authentication**: Test both authenticated and unauthenticated requests
8. **Rate Limiting**: Test rate limit scenarios if applicable

## HTTP Status Codes to Test

- **2xx Success**: 200 (OK), 201 (Created), 204 (No Content)
- **4xx Client Errors**: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 409 (Conflict)
- **5xx Server Errors**: 500 (Internal Server Error), 503 (Service Unavailable)

## Related Recipes

- [Integration Testing](./integration-testing.md)
- [Test Data Generation](./test-data.md)
- [API Documentation](../documentation/api-documentation.md)
