# 🚀 Quick Start Guide

Get started with the Amazon Q Developer Cookbook in 5 minutes!

## What is This Cookbook?

A collection of **proven prompt templates** that help you get the best results from Amazon Q Developer for:
- 🏗️ Creating code (APIs, components, functions)
- ⚡ Optimizing code (performance, refactoring)
- 📝 Writing documentation
- ✅ Generating tests
- 🔒 Implementing security

## Your First Recipe in 3 Steps

### Step 1: Choose a Recipe

Start with something simple, like creating an API endpoint:
👉 [API Endpoint Creation Recipe](./recipes/code-creation/api-endpoint.md)

### Step 2: Customize the Prompt

Copy this template and fill in the brackets:

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

### Step 3: Use with Amazon Q Developer

1. Open your IDE with Amazon Q Developer extension
2. Paste the customized prompt
3. Review the generated code
4. Integrate into your project

**That's it!** You've just used your first recipe. 🎉

## Common Workflows

### Building a New Feature

1. **Create the code**: [API Endpoint](./recipes/code-creation/api-endpoint.md)
2. **Add security**: [Input Validation](./recipes/security/input-validation.md)
3. **Generate tests**: [API Testing](./recipes/testing/api-testing.md)
4. **Write docs**: [API Documentation](./recipes/documentation/api-documentation.md)

### Improving Existing Code

1. **Make it faster**: [Performance Optimization](./recipes/code-optimization/performance.md)
2. **Better errors**: [Error Handling](./recipes/code-optimization/error-handling.md)
3. **Add tests**: [Unit Testing](./recipes/testing/unit-testing.md)

## Recipe Categories

| Category | Use When You Need To... | Start Here |
|----------|------------------------|------------|
| **[Code Creation](./recipes/code-creation/)** | Build something new | [API Endpoint](./recipes/code-creation/api-endpoint.md) |
| **[Code Optimization](./recipes/code-optimization/)** | Improve existing code | [Performance](./recipes/code-optimization/performance.md) |
| **[Documentation](./recipes/documentation/)** | Document your code | [Code Comments](./recipes/documentation/code-comments.md) |
| **[Testing](./recipes/testing/)** | Write tests | [Unit Testing](./recipes/testing/unit-testing.md) |
| **[Security](./recipes/security/)** | Secure your app | [Input Validation](./recipes/security/input-validation.md) |

## Tips for Success

### ✅ DO:
- Be **specific** about your requirements
- Mention your **tech stack** (language, framework, versions)
- Include **examples** when asking for help
- **Iterate** on the output by asking follow-up questions

### ❌ DON'T:
- Use vague prompts like "create an API"
- Forget to mention your framework
- Accept the first output without reviewing
- Skip testing the generated code

## Popular Recipes by Technology

### JavaScript/Node.js Developers
- [API Endpoint Creation](./recipes/code-creation/api-endpoint.md) (Express.js)
- [React Component Creation](./recipes/code-creation/react-component.md)
- [API Testing](./recipes/testing/api-testing.md) (Jest, Supertest)

### Python Developers
- [Python Class Creation](./recipes/code-creation/python-class.md)
- [Unit Testing](./recipes/testing/unit-testing.md) (pytest)
- [Input Validation](./recipes/security/input-validation.md) (FastAPI, Pydantic)

### AWS Developers
- [Lambda Function Creation](./recipes/code-creation/lambda-function.md)
- [Secrets Management](./recipes/security/secrets-management.md) (AWS Secrets Manager)

## Example: End-to-End Feature

Let's build a complete user registration feature:

### 1. Create the API Endpoint (2 minutes)
```
Prompt: "Create an Express.js POST endpoint for /api/users/register 
that accepts email and password, validates input, hashes password, 
saves to database, and returns user object without password"
```

### 2. Add Input Validation (1 minute)
```
Prompt: "Add express-validator middleware to validate email format 
and password strength (min 8 chars, 1 uppercase, 1 number)"
```

### 3. Generate Tests (2 minutes)
```
Prompt: "Create Jest tests for the registration endpoint covering 
success case, duplicate email, invalid email, weak password, and 
database errors"
```

**Total time: ~5 minutes** ⏱️

## Need Help?

- 📚 **Browse all recipes**: [Main README](./README.md)
- 🤝 **Contribute**: [Contributing Guide](./CONTRIBUTING.md)
- 💡 **Examples**: Each recipe has detailed examples
- 🔗 **Related recipes**: Follow the links at the bottom of each recipe

## Next Steps

1. ⭐ Star this repository
2. 📖 Browse the [full recipe collection](./README.md)
3. 🎯 Try a recipe that matches your current task
4. 🔄 Share your feedback and improvements

---

**Happy coding with Amazon Q Developer!** 🚀
