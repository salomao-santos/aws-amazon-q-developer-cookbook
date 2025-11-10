# README Files Recipe

## Description
Create comprehensive, informative README files that help users understand and use your project.

## Prompt Template

```
Create a README.md file for a [PROJECT_TYPE] project with the following details:

Project Name: [NAME]
Description: [BRIEF_DESCRIPTION]
Tech Stack: [TECHNOLOGIES]
Key Features: [LIST_FEATURES]

Include these sections:
- Project title and badges
- Description and purpose
- Features list
- Prerequisites
- Installation instructions
- Usage examples
- Configuration options
- API documentation (if applicable)
- Contributing guidelines
- License information
- Contact/Support information
```

## Example Usage

### Example 1: Library/Package README

**Prompt:**
```
Create a README.md file for a npm package project with the following details:

Project Name: fast-validator
Description: A lightweight, fast validation library for JavaScript with zero dependencies
Tech Stack: TypeScript, Jest, npm
Key Features:
- Schema-based validation
- Custom validators
- TypeScript support
- Zero dependencies
- Async validation support

Include these sections:
- Project title with npm badge and build status badge
- Description and purpose
- Features list with checkmarks
- Prerequisites (Node.js 14+)
- Installation instructions (npm install)
- Quick start usage example
- API documentation with examples for each method
- Configuration options
- Contributing guidelines
- MIT License
- GitHub issues for support
```

**Expected Output:**
```markdown
# fast-validator

![npm version](https://img.shields.io/npm/v/fast-validator.svg)
![build status](https://img.shields.io/github/workflow/status/username/fast-validator/CI)
![license](https://img.shields.io/npm/l/fast-validator.svg)

A lightweight, fast validation library for JavaScript with zero dependencies.

## Features

✅ Schema-based validation  
✅ Custom validators  
✅ Full TypeScript support  
✅ Zero dependencies  
✅ Async validation support  
✅ Comprehensive error messages  

## Prerequisites

- Node.js 14 or higher
- npm or yarn

## Installation

```bash
npm install fast-validator
```

Or with yarn:

```bash
yarn add fast-validator
```

## Quick Start

```javascript
const { Validator } = require('fast-validator');

const schema = {
  email: { type: 'email', required: true },
  age: { type: 'number', min: 18, max: 100 },
  name: { type: 'string', minLength: 2, maxLength: 50 }
};

const validator = new Validator(schema);

const result = validator.validate({
  email: 'user@example.com',
  age: 25,
  name: 'John Doe'
});

if (result.valid) {
  console.log('Validation passed!');
} else {
  console.error('Validation errors:', result.errors);
}
```

## API Documentation

### Creating a Validator

```javascript
const validator = new Validator(schema, options);
```

**Parameters:**
- `schema` (Object): Validation schema definition
- `options` (Object, optional): Configuration options

### Validating Data

```javascript
const result = validator.validate(data);
```

**Returns:**
```javascript
{
  valid: boolean,
  errors: Array<{field: string, message: string}>
}
```

### Schema Types

#### String
```javascript
{
  type: 'string',
  required: true,
  minLength: 5,
  maxLength: 100,
  pattern: /^[a-z]+$/
}
```

#### Number
```javascript
{
  type: 'number',
  required: true,
  min: 0,
  max: 100
}
```

#### Email
```javascript
{
  type: 'email',
  required: true
}
```

### Custom Validators

```javascript
const schema = {
  password: {
    type: 'string',
    custom: (value) => {
      if (!/(?=.*[A-Z])(?=.*[0-9])/.test(value)) {
        return 'Password must contain uppercase and number';
      }
      return true;
    }
  }
};
```

## Configuration

```javascript
const options = {
  strict: true,           // Fail on unknown fields
  abortEarly: false,      // Return all errors, not just first
  messages: {             // Custom error messages
    required: '{field} is required'
  }
};
```

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

Please ensure:
- All tests pass (`npm test`)
- Code follows ESLint rules (`npm run lint`)
- Add tests for new features

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Support

- 📫 Report bugs via [GitHub Issues](https://github.com/username/fast-validator/issues)
- 💬 Ask questions in [Discussions](https://github.com/username/fast-validator/discussions)
- 📖 Read the [Wiki](https://github.com/username/fast-validator/wiki) for detailed guides

## Acknowledgments

- Inspired by other great validation libraries
- Built with ❤️ by the open-source community
```

### Example 2: Web Application README

**Prompt:**
```
Create a README.md file for a web application project with the following details:

Project Name: TaskFlow
Description: A modern task management application with real-time collaboration
Tech Stack: React, Node.js, PostgreSQL, Redis, Docker
Key Features:
- Real-time task updates
- Team collaboration
- File attachments
- Email notifications
- Dark mode support

Include these sections:
- Project title with screenshots
- Description and purpose
- Features list
- Tech stack with icons
- Prerequisites (Node 18+, Docker, PostgreSQL)
- Installation instructions (local and Docker)
- Usage examples with screenshots
- Environment variables configuration
- API documentation link
- Development setup
- Testing instructions
- Deployment guide
- Contributing guidelines
- MIT License
```

## Best Practices

1. **Clear Title**: Make project purpose immediately obvious
2. **Visual Elements**: Include badges, screenshots, GIFs
3. **Quick Start**: Help users get started in under 5 minutes
4. **Examples**: Show real usage examples
5. **Organization**: Use clear sections and hierarchy
6. **Keep Updated**: Update README with project changes
7. **Links**: Provide links to detailed docs, demo, issues
8. **Prerequisites**: List all requirements upfront

## README Sections Checklist

- [ ] Title and badges
- [ ] Description
- [ ] Screenshots/Demo
- [ ] Features
- [ ] Tech stack
- [ ] Prerequisites
- [ ] Installation
- [ ] Usage examples
- [ ] Configuration
- [ ] API docs (if applicable)
- [ ] Testing
- [ ] Contributing
- [ ] License
- [ ] Support/Contact

## Related Recipes

- [API Documentation](./api-documentation.md)
- [Contributing Guidelines](./contributing.md)
- [Architecture Documentation](./architecture.md)
