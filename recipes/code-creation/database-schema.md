# Database Schema Design Recipe

## Description
Design and implement database schemas with proper normalization, indexing, and constraints.

## Prompt Template

```
Create a database schema for [SCHEMA_PURPOSE] with the following requirements:
- Database type: [PostgreSQL/MySQL/DynamoDB/etc.]
- Tables: [LIST_TABLES]
- Relationships: [DESCRIBE_RELATIONSHIPS]
- Include primary keys and foreign keys
- Include appropriate indexes
- Include constraints (NOT NULL, UNIQUE, CHECK)
- Include default values where appropriate
- Follow [DATABASE] naming conventions
- Include migration script format: [SQL/ORM]
- Add comments for documentation
```

## Example Usage

### Example 1: E-commerce Schema

**Prompt:**
```
Create a database schema for an e-commerce platform with the following requirements:
- Database type: PostgreSQL
- Tables: users, products, categories, orders, order_items, reviews
- Relationships: 
  - products have many categories (many-to-many)
  - orders belong to users (one-to-many)
  - orders have many order_items (one-to-many)
  - order_items reference products
  - reviews belong to users and products
- Include primary keys (UUID) and foreign keys with CASCADE options
- Include appropriate indexes on foreign keys, email, product name
- Include constraints (email UNIQUE, price > 0, rating between 1-5)
- Include default values (created_at = NOW(), is_active = true)
- Follow PostgreSQL naming conventions (snake_case)
- Include migration script format: SQL with CREATE TABLE statements
- Add comments for documentation
```

**Expected Output:**
- Complete SQL schema with all tables
- Primary and foreign key definitions
- Index definitions
- Constraint definitions
- Inline comments

### Example 2: DynamoDB Schema

**Prompt:**
```
Create a database schema for a real-time chat application with the following requirements:
- Database type: DynamoDB
- Tables: Users, Conversations, Messages
- Access patterns:
  - Get user by ID
  - Get all conversations for a user
  - Get messages for a conversation (sorted by timestamp)
  - Get recent conversations by last message timestamp
- Include partition keys and sort keys
- Include Global Secondary Indexes (GSI) for access patterns
- Include Local Secondary Indexes (LSI) if needed
- Include TTL attribute for message expiration
- Follow DynamoDB best practices for key design
- Include schema in JSON format
- Add comments for documentation
```

## Best Practices

1. **Normalization**: Follow 3NF unless denormalization is justified
2. **Indexing**: Index foreign keys and frequently queried columns
3. **Constraints**: Use database constraints for data integrity
4. **Naming**: Be consistent with naming conventions
5. **Documentation**: Include comments explaining design decisions
6. **Migrations**: Request version-controlled migration scripts
7. **Performance**: Consider query patterns when designing indexes

## Testing

Use [Database Testing recipes](../testing/database-testing.md) to validate schema.

## Related Recipes

- [Database Optimization](../code-optimization/database-performance.md)
- [Database Testing](../testing/database-testing.md)
- [Security Best Practices](../security/database-security.md)
