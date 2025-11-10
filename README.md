# 🚀 Amazon Q Developer Cookbook

Unlock the full power of Amazon Q Developer! This essential library of tested prompts revolutionizes your workflow. Leverage our recipes to maximize productivity and elevate quality across the board: creating/optimizing code and documentation, generating tests, and integrating robust security practices.

## 📚 Table of Contents

- [Quick Start](./QUICKSTART.md) ⚡ - **New to the cookbook? Start here!**
- [Overview](#overview)
- [Recipe Categories](#recipe-categories)
- [Getting Started](#getting-started)
- [How to Use This Cookbook](#how-to-use-this-cookbook)
- [Recipe Structure](#recipe-structure)
- [Contributing](#contributing)
- [Best Practices](#best-practices)
- [Support](#support)

## 🎯 Overview

The Amazon Q Developer Cookbook is a comprehensive collection of battle-tested prompt templates designed to help developers harness the full capabilities of Amazon Q Developer. Each recipe has been carefully crafted and validated to deliver high-quality results across various development tasks.

### What You'll Find

✅ **Code Creation**: Generate production-ready code for APIs, Lambda functions, React components, and more  
✅ **Code Optimization**: Improve performance, refactor legacy code, and enhance error handling  
✅ **Documentation**: Create comprehensive API docs, README files, and inline comments  
✅ **Testing**: Generate unit tests, integration tests, and API tests with high coverage  
✅ **Security**: Implement input validation, prevent injections, and manage secrets securely  

## 📂 Recipe Categories

### 1. [Code Creation](./recipes/code-creation/)
Generate high-quality code from scratch using proven templates.

- **[API Endpoint Creation](./recipes/code-creation/api-endpoint.md)** - Build RESTful API endpoints with proper error handling
- **[Lambda Function Creation](./recipes/code-creation/lambda-function.md)** - Create AWS Lambda functions with best practices
- **[React Component Creation](./recipes/code-creation/react-component.md)** - Build modern React components with TypeScript
- **[Python Class Creation](./recipes/code-creation/python-class.md)** - Create well-structured Python classes
- **[Database Schema Design](./recipes/code-creation/database-schema.md)** - Design normalized database schemas

### 2. [Code Optimization](./recipes/code-optimization/)
Improve existing code for better performance and maintainability.

- **[Performance Optimization](./recipes/code-optimization/performance.md)** - Reduce complexity and improve speed
- **[Error Handling](./recipes/code-optimization/error-handling.md)** - Implement robust error handling
- **[Code Refactoring](./recipes/code-optimization/refactoring.md)** - Refactor for better maintainability

### 3. [Documentation](./recipes/documentation/)
Create clear, comprehensive documentation for your code.

- **[API Documentation](./recipes/documentation/api-documentation.md)** - Generate OpenAPI/Swagger docs
- **[Code Comments](./recipes/documentation/code-comments.md)** - Add helpful inline documentation
- **[README Files](./recipes/documentation/readme.md)** - Create informative project READMEs

### 4. [Testing](./recipes/testing/)
Generate comprehensive test suites with high coverage.

- **[Unit Testing](./recipes/testing/unit-testing.md)** - Create thorough unit tests
- **[API Testing](./recipes/testing/api-testing.md)** - Test REST and GraphQL APIs

### 5. [Security](./recipes/security/)
Integrate security best practices into your code.

- **[Input Validation](./recipes/security/input-validation.md)** - Validate and sanitize user input
- **[Secrets Management](./recipes/security/secrets-management.md)** - Securely handle sensitive data

## 🚀 Getting Started

### Prerequisites

- Access to Amazon Q Developer (via IDE extension or AWS Console)
- Basic familiarity with your programming language and framework

### Quick Start

1. **Browse the recipes** in the category that matches your task
2. **Choose a recipe** that fits your needs
3. **Copy the prompt template** from the recipe
4. **Customize the template** with your specific requirements
5. **Paste into Amazon Q Developer** and review the output
6. **Iterate and refine** as needed

### Example: Creating an API Endpoint

```
Step 1: Navigate to recipes/code-creation/api-endpoint.md
Step 2: Copy the prompt template
Step 3: Fill in your specific details:
   - Resource name: "tasks"
   - HTTP method: "POST"
   - Request schema: { title, description, dueDate }
   - Framework: "Express.js"
Step 4: Ask Amazon Q Developer
Step 5: Review and integrate the generated code
```

## 📖 How to Use This Cookbook

### Understanding Recipe Structure

Each recipe follows a consistent format:

```markdown
## Description
Brief overview of what the recipe helps you accomplish

## Prompt Template
Ready-to-use template with placeholders [IN_BRACKETS]

## Example Usage
Real-world examples showing the template in action

## Expected Output
Sample outputs you should receive

## Best Practices
Tips for getting optimal results

## Related Recipes
Links to complementary recipes
```

### Customizing Prompts

1. **Replace placeholders** marked with [BRACKETS] with your specific details
2. **Be specific** about technologies, frameworks, and requirements
3. **Include context** like coding standards or constraints
4. **Iterate** by refining your prompt based on initial results

### Example Customization

**Template:**
```
Create a [FRAMEWORK] component for [PURPOSE] with [FEATURES]
```

**Customized:**
```
Create a React component for a data table with sorting, filtering, and pagination
```

## 💡 Best Practices

### 1. Be Specific and Detailed
- ✅ "Create a FastAPI endpoint with Pydantic validation for user registration"
- ❌ "Create an API endpoint"

### 2. Specify Your Tech Stack
Always mention:
- Programming language and version
- Framework and version
- Libraries you want to use
- Code style preferences

### 3. Include Requirements
- Input/output schemas
- Error handling expectations
- Performance requirements
- Security considerations

### 4. Request Documentation
Ask for:
- Inline comments explaining complex logic
- Function/method documentation
- Usage examples

### 5. Iterate and Refine
- Review the output carefully
- Ask follow-up questions to improve code
- Request specific changes or additions

## 🤝 Contributing

We welcome contributions! To add a new recipe:

1. Follow the existing recipe structure
2. Include realistic examples
3. Test your prompts thoroughly
4. Submit a pull request with:
   - Recipe file in appropriate category
   - Updated category README
   - Clear description of the recipe's purpose

### Recipe Quality Guidelines

- **Tested**: All prompts should be tested with Amazon Q Developer
- **Clear**: Use straightforward language and examples
- **Complete**: Include all sections (description, template, examples, best practices)
- **Practical**: Focus on real-world use cases

## 🎓 Tips for Success

1. **Start Simple**: Begin with basic recipes and gradually explore more complex ones
2. **Combine Recipes**: Use multiple recipes together (e.g., code creation + testing)
3. **Learn from Examples**: Study the example outputs to understand patterns
4. **Adapt to Your Needs**: Modify templates to match your specific requirements
5. **Share Feedback**: Let us know what works well and what could be improved

## 📊 Recipe Index by Technology

### Languages
- **JavaScript/TypeScript**: API endpoints, React components, testing
- **Python**: Classes, FastAPI, Lambda functions, data validation
- **SQL**: Database schemas, queries

### Frameworks
- **React**: Component creation, optimization
- **Express.js**: API development, middleware
- **FastAPI**: REST APIs, validation
- **AWS Lambda**: Serverless functions

### Tools
- **Jest**: JavaScript testing
- **pytest**: Python testing
- **Supertest**: API testing
- **OpenAPI/Swagger**: API documentation

## 🔍 Common Use Cases

### Building a New Feature
1. [API Endpoint Creation](./recipes/code-creation/api-endpoint.md)
2. [Input Validation](./recipes/security/input-validation.md)
3. [API Testing](./recipes/testing/api-testing.md)
4. [API Documentation](./recipes/documentation/api-documentation.md)

### Improving Existing Code
1. [Performance Optimization](./recipes/code-optimization/performance.md)
2. [Error Handling](./recipes/code-optimization/error-handling.md)
3. [Code Comments](./recipes/documentation/code-comments.md)
4. [Unit Testing](./recipes/testing/unit-testing.md)

### Security Hardening
1. [Input Validation](./recipes/security/input-validation.md)
2. [Secrets Management](./recipes/security/secrets-management.md)
3. [Error Handling](./recipes/code-optimization/error-handling.md)

## 📞 Support

- **Issues**: Report problems or suggest improvements via GitHub Issues
- **Discussions**: Share your experiences and ask questions in GitHub Discussions
- **Documentation**: Refer to [Amazon Q Developer Documentation](https://docs.aws.amazon.com/amazonq/)

## 📄 License

This cookbook is available under the MIT License. See [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

Created with ❤️ for the developer community. Special thanks to all contributors who help maintain and improve this cookbook.

---

**Ready to revolutionize your development workflow? Start exploring the recipes now!** 🎉
