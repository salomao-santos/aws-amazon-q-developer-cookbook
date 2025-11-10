# Code Comments Recipe

## Description
Generate helpful inline comments that explain complex logic, document assumptions, and improve code maintainability.

## Prompt Template

```
Add helpful comments to the following [LANGUAGE] code:

[PASTE_CODE]

Guidelines:
- Explain WHY, not WHAT (code shows what)
- Document complex algorithms and logic
- Explain non-obvious assumptions
- Add TODOs for future improvements
- Follow [LANGUAGE] comment style conventions
- Include function/method documentation (JSDoc/docstring)
- Avoid stating the obvious
- Keep comments concise and clear
```

## Example Usage

### Example 1: Complex Algorithm Comments

**Prompt:**
```
Add helpful comments to the following Python code:

def find_median_sorted_arrays(nums1, nums2):
    if len(nums1) > len(nums2):
        nums1, nums2 = nums2, nums1
    
    m, n = len(nums1), len(nums2)
    imin, imax, half_len = 0, m, (m + n + 1) // 2
    
    while imin <= imax:
        i = (imin + imax) // 2
        j = half_len - i
        
        if i < m and nums2[j-1] > nums1[i]:
            imin = i + 1
        elif i > 0 and nums1[i-1] > nums2[j]:
            imax = i - 1
        else:
            if i == 0: max_of_left = nums2[j-1]
            elif j == 0: max_of_left = nums1[i-1]
            else: max_of_left = max(nums1[i-1], nums2[j-1])
            
            if (m + n) % 2 == 1:
                return max_of_left
            
            if i == m: min_of_right = nums2[j]
            elif j == n: min_of_right = nums1[i]
            else: min_of_right = min(nums1[i], nums2[j])
            
            return (max_of_left + min_of_right) / 2.0

Guidelines:
- Explain the binary search approach
- Document the algorithm's time complexity
- Explain non-obvious variable meanings (imin, imax, half_len)
- Add function docstring with parameters and return value
- Follow Python PEP 257 docstring conventions
- Avoid stating the obvious
- Keep comments concise
```

**Expected Output:**
```python
def find_median_sorted_arrays(nums1, nums2):
    """
    Find the median of two sorted arrays using binary search.
    
    Time Complexity: O(log(min(m, n))) where m and n are array lengths.
    Space Complexity: O(1)
    
    Args:
        nums1: First sorted array
        nums2: Second sorted array
    
    Returns:
        float: The median value of the combined sorted arrays
    """
    # Ensure nums1 is the smaller array to optimize binary search
    if len(nums1) > len(nums2):
        nums1, nums2 = nums2, nums1
    
    m, n = len(nums1), len(nums2)
    # Binary search bounds on the smaller array
    imin, imax = 0, m
    # Target partition size (half of total elements, rounded up for odd total)
    half_len = (m + n + 1) // 2
    
    while imin <= imax:
        # Partition position in nums1
        i = (imin + imax) // 2
        # Corresponding partition position in nums2
        j = half_len - i
        
        # Binary search logic: adjust partition based on comparison
        if i < m and nums2[j-1] > nums1[i]:
            # i is too small, search right half
            imin = i + 1
        elif i > 0 and nums1[i-1] > nums2[j]:
            # i is too large, search left half
            imax = i - 1
        else:
            # Found correct partition
            # Find max element on left side of partition
            if i == 0: max_of_left = nums2[j-1]
            elif j == 0: max_of_left = nums1[i-1]
            else: max_of_left = max(nums1[i-1], nums2[j-1])
            
            # For odd total length, median is max of left side
            if (m + n) % 2 == 1:
                return max_of_left
            
            # For even total length, median is average of max(left) and min(right)
            if i == m: min_of_right = nums2[j]
            elif j == n: min_of_right = nums1[i]
            else: min_of_right = min(nums1[i], nums2[j])
            
            return (max_of_left + min_of_right) / 2.0
```

### Example 2: Business Logic Comments

**Prompt:**
```
Add helpful comments to the following JavaScript code:

function calculateShippingCost(order) {
  const baseRate = 5.99;
  const weightRate = 0.50;
  const distanceRate = 0.10;
  
  let cost = baseRate;
  
  if (order.weight > 10) {
    cost += (order.weight - 10) * weightRate;
  }
  
  if (order.distance > 50) {
    cost += (order.distance - 50) * distanceRate;
  }
  
  if (order.isPriority) {
    cost *= 1.5;
  }
  
  if (order.total > 100) {
    cost = 0;
  }
  
  return Math.round(cost * 100) / 100;
}

Guidelines:
- Explain business rules and assumptions
- Document magic numbers
- Add JSDoc function documentation
- Explain conditional logic reasoning
- Follow JavaScript comment conventions
- Keep comments helpful and concise
```

**Expected Output:**
```javascript
/**
 * Calculate shipping cost based on order weight, distance, and total.
 * 
 * Business Rules:
 * - Free shipping for orders over $100
 * - Base rate applies to all orders under 10 lbs and 50 miles
 * - Additional charges for excess weight and distance
 * - Priority shipping costs 50% more
 * 
 * @param {Object} order - Order details
 * @param {number} order.weight - Package weight in pounds
 * @param {number} order.distance - Shipping distance in miles
 * @param {boolean} order.isPriority - Whether priority shipping is requested
 * @param {number} order.total - Order total in dollars
 * @returns {number} Shipping cost rounded to 2 decimal places
 */
function calculateShippingCost(order) {
  // Standard shipping rates (in USD)
  const baseRate = 5.99;        // Base shipping fee for orders ≤10 lbs, ≤50 miles
  const weightRate = 0.50;       // Additional charge per pound over 10 lbs
  const distanceRate = 0.10;     // Additional charge per mile over 50 miles
  
  let cost = baseRate;
  
  // Add surcharge for packages over 10 pounds
  if (order.weight > 10) {
    cost += (order.weight - 10) * weightRate;
  }
  
  // Add surcharge for long-distance shipping (over 50 miles)
  if (order.distance > 50) {
    cost += (order.distance - 50) * distanceRate;
  }
  
  // Priority shipping adds 50% to total cost
  if (order.isPriority) {
    cost *= 1.5;
  }
  
  // Free shipping promotion for orders over $100
  if (order.total > 100) {
    cost = 0;
  }
  
  // Round to 2 decimal places for currency
  return Math.round(cost * 100) / 100;
}
```

## Best Practices

1. **Explain Why**: Focus on intent and business logic, not syntax
2. **Document Assumptions**: Make implicit assumptions explicit
3. **Complex Logic**: Break down algorithms and formulas
4. **TODOs**: Mark areas for future improvement
5. **Avoid Obvious**: Don't comment self-explanatory code
6. **Keep Updated**: Update comments when code changes
7. **Be Concise**: Clear and brief is better than verbose

## Comment Types

- **Function/Method Docs**: JSDoc, docstrings, XML comments
- **Inline Comments**: Brief explanations within code
- **Block Comments**: Multi-line explanations for sections
- **TODO Comments**: Future improvements or known issues
- **FIXME Comments**: Known bugs or problems

## Related Recipes

- [API Documentation](./api-documentation.md)
- [README Files](./readme.md)
- [Code Refactoring](../code-optimization/refactoring.md)
