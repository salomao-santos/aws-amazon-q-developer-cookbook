# API Endpoint Creation Recipe

## Description
Create robust RESTful API endpoints with proper error handling, validation, and documentation.

## Prompt Template

```
Create a REST API endpoint for [RESOURCE_NAME] with the following requirements:
- HTTP Method: [GET/POST/PUT/DELETE]
- Path: /api/[version]/[resource]
- Request body/parameters: [SPECIFY_SCHEMA]
- Response format: JSON
- Include input validation
- Include error handling for common scenarios (400, 404, 500)
- Add proper logging
- Follow [FRAMEWORK] best practices
- Include OpenAPI/Swagger documentation comments
```

## Example Usage

### Example 1: User Registration Endpoint

**Prompt:**
```
Create a REST API endpoint for user registration with the following requirements:
- HTTP Method: POST
- Path: /api/v1/users/register
- Request body: { email, password, firstName, lastName }
- Response format: JSON
- Include email validation
- Include error handling for duplicate users (409), invalid input (400), server errors (500)
- Add proper logging
- Follow Express.js best practices
- Include OpenAPI/Swagger documentation comments
```

**Expected Output:**
- Complete endpoint implementation with route handler
- Input validation middleware
- Error handling middleware
- Logging statements
- API documentation comments

### Example 2: Product Search Endpoint

**Prompt:**
```
Create a REST API endpoint for product search with the following requirements:
- HTTP Method: GET
- Path: /api/v1/products/search
- Query parameters: { query, category, minPrice, maxPrice, limit, offset }
- Response format: JSON with pagination metadata
- Include query parameter validation
- Include error handling for invalid parameters (400), not found (404), server errors (500)
- Add proper logging
- Follow FastAPI best practices
- Include OpenAPI/Swagger documentation comments
```

## Best Practices

1. **Be Specific**: Clearly define request/response schemas
2. **Specify Framework**: Mention your framework (Express, FastAPI, Spring Boot, etc.)
3. **Include Validation**: Always request input validation logic
4. **Error Scenarios**: List expected error conditions
5. **Documentation**: Request inline documentation and API specs

## Testing

After generating code, use the [Test Generation recipes](../testing/api-testing.md) to create comprehensive tests.

## Related Recipes

- [Error Handling](../code-optimization/error-handling.md)
- [API Testing](../testing/api-testing.md)
- [Security Best Practices](../security/api-security.md)
