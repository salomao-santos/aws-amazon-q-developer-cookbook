# Unit Testing Recipe

## Description
Generate comprehensive unit tests for functions, classes, and modules with proper assertions and edge cases.

## Prompt Template

```
Create unit tests for the following [LANGUAGE] code using [TEST_FRAMEWORK]:

[PASTE_CODE]

Requirements:
- Test framework: [Jest/pytest/JUnit/etc.]
- Test happy path scenarios
- Test edge cases (empty input, null, boundary values)
- Test error conditions
- Include test descriptions
- Use appropriate assertions
- Mock external dependencies
- Aim for [XX]% code coverage
- Follow [FRAMEWORK] best practices
```

## Example Usage

### Example 1: JavaScript Function Testing

**Prompt:**
```
Create unit tests for the following JavaScript code using Jest:

function calculateDiscount(price, discountPercent, customerType) {
  if (price < 0 || discountPercent < 0 || discountPercent > 100) {
    throw new Error('Invalid input');
  }
  
  let discount = price * (discountPercent / 100);
  
  if (customerType === 'premium') {
    discount *= 1.1; // 10% bonus for premium customers
  }
  
  return Math.min(discount, price);
}

Requirements:
- Test framework: Jest
- Test happy path (valid inputs)
- Test edge cases (0 price, 0 discount, 100% discount, boundary values)
- Test error conditions (negative price, invalid discount percent)
- Test premium customer bonus
- Include descriptive test names
- Use appropriate Jest assertions (toThrow, toBeCloseTo for decimals)
- Aim for 100% code coverage
- Follow Jest best practices
```

**Expected Output:**
```javascript
describe('calculateDiscount', () => {
  describe('happy path', () => {
    test('calculates discount correctly for regular customer', () => {
      const result = calculateDiscount(100, 20, 'regular');
      expect(result).toBe(20);
    });
    
    test('calculates discount with bonus for premium customer', () => {
      const result = calculateDiscount(100, 20, 'premium');
      expect(result).toBe(22); // 20% discount + 10% bonus = 22
    });
    
    test('handles decimal percentages correctly', () => {
      const result = calculateDiscount(99.99, 15.5, 'regular');
      expect(result).toBeCloseTo(15.498, 2);
    });
  });
  
  describe('edge cases', () => {
    test('returns 0 when price is 0', () => {
      const result = calculateDiscount(0, 20, 'regular');
      expect(result).toBe(0);
    });
    
    test('returns 0 when discount percent is 0', () => {
      const result = calculateDiscount(100, 0, 'regular');
      expect(result).toBe(0);
    });
    
    test('returns price when discount is 100%', () => {
      const result = calculateDiscount(100, 100, 'regular');
      expect(result).toBe(100);
    });
    
    test('caps discount at price value', () => {
      // Premium customer with high discount could exceed price
      const result = calculateDiscount(50, 100, 'premium');
      expect(result).toBe(50); // Capped at price
    });
    
    test('handles very small prices', () => {
      const result = calculateDiscount(0.01, 50, 'regular');
      expect(result).toBeCloseTo(0.005, 3);
    });
  });
  
  describe('error conditions', () => {
    test('throws error for negative price', () => {
      expect(() => calculateDiscount(-10, 20, 'regular'))
        .toThrow('Invalid input');
    });
    
    test('throws error for negative discount', () => {
      expect(() => calculateDiscount(100, -5, 'regular'))
        .toThrow('Invalid input');
    });
    
    test('throws error for discount over 100', () => {
      expect(() => calculateDiscount(100, 101, 'regular'))
        .toThrow('Invalid input');
    });
  });
  
  describe('customer types', () => {
    test('handles undefined customer type as regular', () => {
      const result = calculateDiscount(100, 20, undefined);
      expect(result).toBe(20);
    });
    
    test('handles unknown customer type as regular', () => {
      const result = calculateDiscount(100, 20, 'gold');
      expect(result).toBe(20);
    });
  });
});
```

### Example 2: Python Class Testing

**Prompt:**
```
Create unit tests for the following Python class using pytest:

class ShoppingCart:
    def __init__(self):
        self.items = []
    
    def add_item(self, item_id, name, price, quantity=1):
        if price < 0:
            raise ValueError("Price cannot be negative")
        if quantity < 1:
            raise ValueError("Quantity must be at least 1")
        
        self.items.append({
            'id': item_id,
            'name': name,
            'price': price,
            'quantity': quantity
        })
    
    def get_total(self):
        return sum(item['price'] * item['quantity'] for item in self.items)
    
    def remove_item(self, item_id):
        self.items = [item for item in self.items if item['id'] != item_id]

Requirements:
- Test framework: pytest
- Test all methods (add_item, get_total, remove_item)
- Test edge cases (empty cart, multiple items, duplicates)
- Test error conditions (negative price, invalid quantity)
- Use pytest fixtures for setup
- Use appropriate assertions
- Mock not needed (no external dependencies)
- Aim for 100% code coverage
- Follow pytest best practices with proper test organization
```

**Expected Output:**
```python
import pytest
from shopping_cart import ShoppingCart


class TestShoppingCart:
    """Test suite for ShoppingCart class"""
    
    @pytest.fixture
    def cart(self):
        """Fixture providing a fresh ShoppingCart instance"""
        return ShoppingCart()
    
    @pytest.fixture
    def cart_with_items(self):
        """Fixture providing a cart with sample items"""
        cart = ShoppingCart()
        cart.add_item(1, "Apple", 1.50, 3)
        cart.add_item(2, "Banana", 0.75, 5)
        return cart
    
    class TestAddItem:
        """Tests for add_item method"""
        
        def test_add_single_item(self, cart):
            """Should add item with all details"""
            cart.add_item(1, "Apple", 1.50, 2)
            
            assert len(cart.items) == 1
            assert cart.items[0]['id'] == 1
            assert cart.items[0]['name'] == "Apple"
            assert cart.items[0]['price'] == 1.50
            assert cart.items[0]['quantity'] == 2
        
        def test_add_item_default_quantity(self, cart):
            """Should use quantity=1 by default"""
            cart.add_item(1, "Apple", 1.50)
            
            assert cart.items[0]['quantity'] == 1
        
        def test_add_multiple_items(self, cart):
            """Should handle multiple items"""
            cart.add_item(1, "Apple", 1.50)
            cart.add_item(2, "Banana", 0.75)
            
            assert len(cart.items) == 2
        
        def test_add_duplicate_item_ids(self, cart):
            """Should allow duplicate item IDs (separate entries)"""
            cart.add_item(1, "Apple", 1.50, 2)
            cart.add_item(1, "Apple", 1.50, 3)
            
            assert len(cart.items) == 2
        
        def test_negative_price_raises_error(self, cart):
            """Should raise ValueError for negative price"""
            with pytest.raises(ValueError, match="Price cannot be negative"):
                cart.add_item(1, "Apple", -1.50)
        
        def test_zero_quantity_raises_error(self, cart):
            """Should raise ValueError for quantity less than 1"""
            with pytest.raises(ValueError, match="Quantity must be at least 1"):
                cart.add_item(1, "Apple", 1.50, 0)
        
        def test_negative_quantity_raises_error(self, cart):
            """Should raise ValueError for negative quantity"""
            with pytest.raises(ValueError, match="Quantity must be at least 1"):
                cart.add_item(1, "Apple", 1.50, -5)
        
        def test_zero_price_is_valid(self, cart):
            """Should accept zero price (free items)"""
            cart.add_item(1, "Free Sample", 0.00)
            
            assert cart.items[0]['price'] == 0.00
    
    class TestGetTotal:
        """Tests for get_total method"""
        
        def test_empty_cart_total(self, cart):
            """Should return 0 for empty cart"""
            assert cart.get_total() == 0
        
        def test_single_item_total(self, cart):
            """Should calculate total for single item"""
            cart.add_item(1, "Apple", 1.50, 3)
            
            assert cart.get_total() == 4.50
        
        def test_multiple_items_total(self, cart_with_items):
            """Should sum all items correctly"""
            # 3 apples at 1.50 = 4.50
            # 5 bananas at 0.75 = 3.75
            # Total = 8.25
            assert cart_with_items.get_total() == 8.25
        
        def test_total_with_decimal_precision(self, cart):
            """Should handle decimal precision correctly"""
            cart.add_item(1, "Item", 1.99, 3)
            
            assert cart.get_total() == pytest.approx(5.97)
    
    class TestRemoveItem:
        """Tests for remove_item method"""
        
        def test_remove_existing_item(self, cart_with_items):
            """Should remove item by ID"""
            cart_with_items.remove_item(1)
            
            assert len(cart_with_items.items) == 1
            assert cart_with_items.items[0]['id'] == 2
        
        def test_remove_nonexistent_item(self, cart_with_items):
            """Should handle removing non-existent item gracefully"""
            cart_with_items.remove_item(999)
            
            assert len(cart_with_items.items) == 2  # No change
        
        def test_remove_from_empty_cart(self, cart):
            """Should handle empty cart gracefully"""
            cart.remove_item(1)
            
            assert len(cart.items) == 0
        
        def test_remove_duplicate_ids(self, cart):
            """Should remove all items with matching ID"""
            cart.add_item(1, "Apple", 1.50, 2)
            cart.add_item(1, "Apple", 1.50, 3)
            cart.add_item(2, "Banana", 0.75)
            
            cart.remove_item(1)
            
            assert len(cart.items) == 1
            assert cart.items[0]['id'] == 2
```

## Best Practices

1. **Descriptive Names**: Use clear, descriptive test names
2. **AAA Pattern**: Arrange, Act, Assert structure
3. **One Assertion**: Focus each test on one behavior
4. **Edge Cases**: Test boundaries and special values
5. **Error Cases**: Test all error conditions
6. **Fixtures/Setup**: Use proper test fixtures for setup
7. **Independence**: Tests should not depend on each other
8. **Coverage**: Aim for high code coverage (80%+)

## Common Test Patterns

- **Happy Path**: Valid inputs, expected behavior
- **Edge Cases**: Boundary values, empty inputs, special values
- **Error Cases**: Invalid inputs, exception handling
- **State Changes**: Verify state before and after
- **Return Values**: Assert correct outputs

## Related Recipes

- [Test Data Generation](./test-data.md)
- [Integration Testing](./integration-testing.md)
- [Code Coverage](./coverage.md)
