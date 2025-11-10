# API Documentation Recipe

## Description
Generate comprehensive API documentation including endpoints, parameters, responses, and examples.

## Prompt Template

```
Generate API documentation for the following [LANGUAGE/FRAMEWORK] code:

[PASTE_CODE]

Include:
- Endpoint description and purpose
- HTTP method and path
- Request parameters (path, query, body)
- Request body schema with types
- Response format and status codes
- Error responses and codes
- Authentication requirements
- Example requests and responses
- Rate limiting information (if applicable)
- Format: [OpenAPI/Swagger/Markdown/JSDoc]
```

## Example Usage

### Example 1: REST API Endpoint Documentation

**Prompt:**
```
Generate API documentation for the following Express.js code:

router.post('/api/v1/products', authenticate, async (req, res) => {
  try {
    const product = await Product.create({
      name: req.body.name,
      description: req.body.description,
      price: req.body.price,
      categoryId: req.body.categoryId
    });
    res.status(201).json(product);
  } catch (error) {
    if (error.name === 'ValidationError') {
      res.status(400).json({ error: error.message });
    } else {
      res.status(500).json({ error: 'Internal server error' });
    }
  }
});

Include:
- Endpoint description and purpose
- HTTP method (POST) and path
- Request body schema with types (name: string, description: string, price: number, categoryId: number)
- Response format (JSON) and status codes (201, 400, 500)
- Error responses with examples
- Authentication requirements (Bearer token)
- Example requests and responses
- Format: OpenAPI 3.0 YAML
```

**Expected Output:**
```yaml
/api/v1/products:
  post:
    summary: Create a new product
    description: Creates a new product in the catalog
    security:
      - BearerAuth: []
    requestBody:
      required: true
      content:
        application/json:
          schema:
            type: object
            required:
              - name
              - price
              - categoryId
            properties:
              name:
                type: string
                description: Product name
                example: "Wireless Mouse"
              description:
                type: string
                description: Product description
                example: "Ergonomic wireless mouse with USB receiver"
              price:
                type: number
                format: decimal
                description: Product price in USD
                example: 29.99
              categoryId:
                type: integer
                description: Category identifier
                example: 5
    responses:
      '201':
        description: Product created successfully
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Product'
      '400':
        description: Validation error
        content:
          application/json:
            schema:
              type: object
              properties:
                error:
                  type: string
                  example: "Validation failed: name is required"
      '401':
        description: Authentication required
      '500':
        description: Internal server error
```

### Example 2: GraphQL API Documentation

**Prompt:**
```
Generate API documentation for the following GraphQL resolver:

const resolvers = {
  Query: {
    user: async (_, { id }, { dataSources }) => {
      return dataSources.userAPI.getUserById(id);
    },
  },
  Mutation: {
    createUser: async (_, { input }, { dataSources }) => {
      return dataSources.userAPI.createUser(input);
    },
  },
};

Schema:
type Query {
  user(id: ID!): User
}

type Mutation {
  createUser(input: CreateUserInput!): User
}

input CreateUserInput {
  email: String!
  firstName: String!
  lastName: String!
}

type User {
  id: ID!
  email: String!
  firstName: String!
  lastName: String!
  createdAt: DateTime!
}

Include:
- Query/Mutation descriptions
- Input parameter types and validation
- Return types
- Error scenarios
- Example queries with responses
- Format: Markdown
```

## Best Practices

1. **Be Complete**: Document all parameters, responses, and errors
2. **Include Examples**: Provide realistic request/response examples
3. **Specify Types**: Clearly define data types and constraints
4. **Error Handling**: Document all possible error responses
5. **Authentication**: Clearly specify auth requirements
6. **Versioning**: Include API version information
7. **Keep Updated**: Regenerate docs when API changes

## Tools Integration

- **OpenAPI/Swagger**: For REST APIs, request OpenAPI 3.0 format
- **GraphQL**: Use built-in introspection or markdown docs
- **Postman**: Export collections with examples
- **API Blueprint**: For detailed API specifications

## Related Recipes

- [Code Comments](./code-comments.md)
- [README Files](./readme.md)
- [API Testing](../testing/api-testing.md)
