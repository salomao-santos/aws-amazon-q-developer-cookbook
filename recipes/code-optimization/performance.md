# Performance Optimization Recipe

## Description
Improve code performance by identifying bottlenecks and applying optimization techniques.

## Prompt Template

```
Optimize the following [LANGUAGE] code for better performance:

[PASTE_CODE]

Focus on:
- Algorithmic complexity reduction
- [SPECIFIC_OPTIMIZATION: caching/parallel processing/lazy loading]
- Memory efficiency
- [FRAMEWORK]-specific optimizations
- Maintain readability and functionality
- Add performance comments explaining optimizations
```

## Example Usage

### Example 1: Algorithm Optimization

**Prompt:**
```
Optimize the following Python code for better performance:

def find_duplicates(numbers):
    duplicates = []
    for i in range(len(numbers)):
        for j in range(i + 1, len(numbers)):
            if numbers[i] == numbers[j] and numbers[i] not in duplicates:
                duplicates.append(numbers[i])
    return duplicates

Focus on:
- Algorithmic complexity reduction (currently O(n²))
- Memory efficiency using sets
- Maintain readability and functionality
- Add performance comments explaining optimizations
```

**Expected Improvements:**
- Reduced time complexity from O(n²) to O(n)
- Better memory usage with set-based approach
- Clearer code structure

### Example 2: React Component Optimization

**Prompt:**
```
Optimize the following React component for better performance:

function UserList({ users, onUserClick }) {
  return (
    <div>
      {users.map(user => (
        <div key={user.id} onClick={() => onUserClick(user.id)}>
          {user.name} - {user.email}
        </div>
      ))}
    </div>
  );
}

Focus on:
- React.memo usage
- useCallback for event handlers
- Prevent unnecessary re-renders
- React-specific optimizations
- Maintain readability and functionality
- Add performance comments explaining optimizations
```

**Expected Improvements:**
- Memoized component to prevent unnecessary renders
- Optimized callbacks
- Better performance with large lists

### Example 3: Database Query Optimization

**Prompt:**
```
Optimize the following Node.js code for better performance:

async function getUsersWithOrders() {
  const users = await db.query('SELECT * FROM users');
  
  for (const user of users) {
    user.orders = await db.query('SELECT * FROM orders WHERE user_id = ?', [user.id]);
    
    for (const order of user.orders) {
      order.items = await db.query('SELECT * FROM order_items WHERE order_id = ?', [order.id]);
    }
  }
  
  return users;
}

Focus on:
- Eliminate N+1 query problem
- Use JOIN operations
- Reduce database round trips
- Maintain readability and functionality
- Add performance comments explaining optimizations
```

**Expected Improvements:**
- Single query with JOINs instead of multiple queries
- Dramatically reduced database round trips
- Better performance with large datasets

## Best Practices

1. **Measure First**: Identify actual bottlenecks before optimizing
2. **Preserve Behavior**: Ensure optimizations don't change functionality
3. **Document Changes**: Add comments explaining optimization techniques
4. **Test Performance**: Verify improvements with benchmarks
5. **Balance Readability**: Don't sacrifice clarity for minor gains

## Measuring Impact

After optimization, compare:
- **Execution Time**: Before vs. after runtime
- **Memory Usage**: Peak memory consumption
- **Complexity**: Big O notation improvement
- **Database Queries**: Number of queries and execution time

## Related Recipes

- [Memory Optimization](./memory.md)
- [Database Performance](./database-performance.md)
- [Testing Performance](../testing/performance-testing.md)
