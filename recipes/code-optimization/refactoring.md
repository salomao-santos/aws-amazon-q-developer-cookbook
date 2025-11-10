# Code Refactoring Recipe

## Description
Refactor code to improve maintainability, readability, and adherence to best practices.

## Prompt Template

```
Refactor the following [LANGUAGE] code to improve [ASPECT: maintainability/readability/testability]:

[PASTE_CODE]

Apply these refactoring techniques:
- [TECHNIQUE: Extract method/class/constant]
- Follow [DESIGN_PATTERN] pattern if applicable
- Apply SOLID principles
- Improve naming conventions
- Reduce code duplication
- Simplify complex logic
- Preserve original functionality
- Add comments for complex sections
```

## Example Usage

### Example 1: Extract Method Refactoring

**Prompt:**
```
Refactor the following JavaScript code to improve readability and maintainability:

function processOrder(order) {
  // Validate order
  if (!order.items || order.items.length === 0) {
    throw new Error('Order must have items');
  }
  if (!order.customerId) {
    throw new Error('Order must have customer');
  }
  
  // Calculate total
  let total = 0;
  for (const item of order.items) {
    total += item.price * item.quantity;
  }
  
  // Apply discount
  if (order.couponCode) {
    if (order.couponCode === 'SAVE10') {
      total *= 0.9;
    } else if (order.couponCode === 'SAVE20') {
      total *= 0.8;
    }
  }
  
  // Calculate tax
  const taxRate = 0.08;
  const tax = total * taxRate;
  total += tax;
  
  return { total, tax };
}

Apply these refactoring techniques:
- Extract method for validation, calculation, discount, tax
- Reduce code duplication
- Improve naming conventions
- Simplify complex logic
- Preserve original functionality
- Add JSDoc comments for extracted methods
```

**Expected Improvements:**
- Separate methods for each responsibility
- Better code organization
- Easier to test individual parts
- Clearer intent

### Example 2: Strategy Pattern Refactoring

**Prompt:**
```
Refactor the following Python code to improve extensibility:

class PaymentProcessor:
    def process_payment(self, amount, payment_type):
        if payment_type == 'credit_card':
            # Process credit card
            fee = amount * 0.029
            total = amount + fee
            return self._charge_credit_card(total)
        elif payment_type == 'paypal':
            # Process PayPal
            fee = amount * 0.034
            total = amount + fee
            return self._charge_paypal(total)
        elif payment_type == 'bank_transfer':
            # Process bank transfer
            fee = 2.50
            total = amount + fee
            return self._process_bank_transfer(total)
        else:
            raise ValueError(f'Unknown payment type: {payment_type}')

Apply these refactoring techniques:
- Follow Strategy pattern
- Apply SOLID principles (Open/Closed)
- Reduce code duplication
- Improve extensibility for new payment types
- Preserve original functionality
- Add docstrings for classes and methods
```

**Expected Improvements:**
- Strategy pattern implementation
- Easy to add new payment methods
- Better separation of concerns
- Follows Open/Closed principle

### Example 3: Simplify Complex Logic

**Prompt:**
```
Refactor the following code to simplify complex conditional logic:

function getUserPermissions(user, resource) {
  if (user.role === 'admin') {
    return ['read', 'write', 'delete'];
  } else if (user.role === 'editor') {
    if (resource.ownerId === user.id) {
      return ['read', 'write', 'delete'];
    } else {
      return ['read', 'write'];
    }
  } else if (user.role === 'viewer') {
    if (resource.isPublic) {
      return ['read'];
    } else if (resource.ownerId === user.id) {
      return ['read'];
    } else {
      return [];
    }
  } else {
    return [];
  }
}

Apply these refactoring techniques:
- Simplify nested conditionals
- Use early returns
- Consider lookup table or strategy pattern
- Improve naming conventions
- Preserve original functionality
- Add comments explaining permission logic
```

**Expected Improvements:**
- Simplified conditional logic
- Better readability
- Easier to maintain and extend

## Best Practices

1. **Small Steps**: Refactor incrementally, not all at once
2. **Preserve Behavior**: Don't change functionality while refactoring
3. **Test Coverage**: Ensure tests pass before and after
4. **Code Smells**: Target specific code smells (long methods, duplicated code)
5. **SOLID Principles**: Apply where appropriate
6. **Readability**: Prioritize code clarity
7. **Documentation**: Update comments and docs after refactoring

## Common Refactoring Patterns

- **Extract Method**: Break long methods into smaller ones
- **Extract Class**: Move related code into new class
- **Replace Conditional with Polymorphism**: Use inheritance/strategy pattern
- **Introduce Parameter Object**: Group related parameters
- **Replace Magic Numbers**: Use named constants

## Related Recipes

- [Testing Before Refactoring](../testing/refactoring-tests.md)
- [Design Patterns](./design-patterns.md)
- [Code Review](./code-review.md)
