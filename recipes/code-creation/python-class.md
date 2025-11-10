# Python Class Creation Recipe

## Description
Create well-structured, maintainable Python classes with proper encapsulation, type hints, and documentation.

## Prompt Template

```
Create a Python class for [CLASS_PURPOSE] with the following requirements:
- Class name: [ClassName]
- Attributes: [LIST_ATTRIBUTES_WITH_TYPES]
- Methods: [LIST_METHODS_WITH_SIGNATURES]
- Include type hints (Python 3.10+)
- Include docstrings (Google/NumPy style)
- Include property decorators where appropriate
- Include __init__, __str__, __repr__ methods
- Include data validation in setters
- Follow PEP 8 style guide
- Include error handling
```

## Example Usage

### Example 1: User Model Class

**Prompt:**
```
Create a Python class for a User model with the following requirements:
- Class name: User
- Attributes: id (int), email (str), first_name (str), last_name (str), created_at (datetime), is_active (bool)
- Methods: full_name() -> str, validate_email() -> bool, to_dict() -> dict, from_dict(data: dict) -> User
- Include type hints (Python 3.10+)
- Include docstrings (Google style)
- Include property decorators for computed properties
- Include __init__, __str__, __repr__ methods
- Include email validation in setter
- Follow PEP 8 style guide
- Include error handling for invalid email formats
```

**Expected Output:**
- Complete class definition
- Type hints for all methods and attributes
- Docstrings for class and methods
- Data validation logic
- Property decorators

### Example 2: Database Connection Pool Class

**Prompt:**
```
Create a Python class for a database connection pool with the following requirements:
- Class name: ConnectionPool
- Attributes: max_connections (int), current_connections (int), connection_string (str), available_connections (Queue)
- Methods: get_connection() -> Connection, release_connection(conn: Connection), close_all(), __enter__, __exit__
- Include type hints (Python 3.10+)
- Include docstrings (Google style)
- Include property decorators for read-only properties
- Include __init__ method with connection pool initialization
- Include validation for max_connections > 0
- Follow PEP 8 style guide
- Include error handling for connection failures, pool exhaustion
- Implement context manager protocol
```

## Best Practices

1. **Type Hints**: Always include type hints for better IDE support
2. **Docstrings**: Use consistent docstring style (Google or NumPy)
3. **Encapsulation**: Use private attributes (underscore prefix) when appropriate
4. **Properties**: Use @property for computed attributes
5. **Validation**: Include validation in setters or __init__
6. **Magic Methods**: Implement __str__, __repr__, __eq__ when useful
7. **Context Managers**: Use __enter__ and __exit__ for resource management

## Testing

Use [Python Testing recipes](../testing/python-testing.md) to create unit tests.

## Related Recipes

- [Code Optimization](../code-optimization/python-performance.md)
- [Python Testing](../testing/python-testing.md)
- [Error Handling](../code-optimization/error-handling.md)
