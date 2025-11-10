# Contributing to Amazon Q Developer Cookbook

Thank you for your interest in contributing! This cookbook thrives on community contributions.

## How to Contribute

### 1. Adding a New Recipe

New recipes are always welcome! Follow these steps:

1. **Choose the Right Category**
   - `code-creation/`: For generating new code
   - `code-optimization/`: For improving existing code
   - `documentation/`: For creating documentation
   - `testing/`: For test generation
   - `security/`: For security implementations

2. **Create Your Recipe File**
   - Use kebab-case for filenames (e.g., `api-endpoint.md`)
   - Follow the standard recipe structure (see template below)

3. **Test Your Prompts**
   - Test all prompts with Amazon Q Developer
   - Verify outputs match expectations
   - Include realistic examples

4. **Update Category README**
   - Add your recipe to the category's README.md
   - Include a brief description

5. **Submit a Pull Request**
   - Clear description of the recipe's purpose
   - Links to any related issues

### Recipe Template

```markdown
# [Recipe Name] Recipe

## Description
[Brief overview of what this recipe accomplishes]

## Prompt Template

\```
[Your prompt template with [PLACEHOLDERS]]

Requirements:
- [Requirement 1]
- [Requirement 2]
\```

## Example Usage

### Example 1: [Scenario Name]

**Prompt:**
\```
[Complete example prompt]
\```

**Expected Output:**
\```[language]
[Sample output code]
\```

## Best Practices

1. **Practice 1**: Description
2. **Practice 2**: Description

## Related Recipes

- [Related Recipe 1](../category/recipe.md)
- [Related Recipe 2](../category/recipe.md)
```

### 2. Improving Existing Recipes

Found a way to improve a recipe? Great!

- Fix typos or unclear instructions
- Add more examples
- Update best practices
- Improve prompt templates

### 3. Reporting Issues

If you find a problem:

1. Check if it's already reported
2. Create a new issue with:
   - Clear description
   - Recipe name and location
   - Expected vs actual behavior
   - Steps to reproduce

## Quality Guidelines

### Recipe Quality Checklist

- [ ] Recipe has a clear, descriptive title
- [ ] Description explains the recipe's purpose
- [ ] Prompt template includes all necessary placeholders
- [ ] At least 2 realistic examples provided
- [ ] Expected outputs are complete and correct
- [ ] Best practices section includes valuable tips
- [ ] Related recipes are linked
- [ ] All prompts tested with Amazon Q Developer
- [ ] Markdown formatting is correct
- [ ] Code examples use proper syntax highlighting

### Writing Style

- **Clear**: Use simple, straightforward language
- **Concise**: Avoid unnecessary verbosity
- **Practical**: Focus on real-world use cases
- **Consistent**: Follow existing recipe patterns
- **Professional**: Maintain a helpful, professional tone

### Code Standards

- Use proper syntax highlighting in code blocks
- Include complete, runnable examples when possible
- Follow language-specific best practices
- Add comments to explain complex logic

## Pull Request Process

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b recipe/my-new-recipe`
3. **Make your changes**
4. **Test thoroughly**
5. **Commit with clear messages**: `git commit -m "Add recipe for GraphQL schema generation"`
6. **Push to your fork**: `git push origin recipe/my-new-recipe`
7. **Open a Pull Request**

### PR Description Template

```markdown
## Description
[What does this PR add/fix/improve?]

## Type of Change
- [ ] New recipe
- [ ] Recipe improvement
- [ ] Bug fix
- [ ] Documentation update

## Recipe Information (if applicable)
- **Category**: [code-creation/code-optimization/etc.]
- **Recipe Name**: [Name]
- **Technologies**: [Languages/frameworks covered]

## Testing
- [ ] Tested all prompts with Amazon Q Developer
- [ ] Verified expected outputs
- [ ] Checked related recipes for consistency

## Checklist
- [ ] Followed recipe template structure
- [ ] Updated category README
- [ ] Checked spelling and grammar
- [ ] Added realistic examples
- [ ] Included best practices
```

## Code of Conduct

### Our Standards

- Be respectful and inclusive
- Welcome newcomers
- Accept constructive criticism gracefully
- Focus on what's best for the community
- Show empathy towards other contributors

### Unacceptable Behavior

- Harassment or discriminatory language
- Trolling or insulting comments
- Personal or political attacks
- Publishing others' private information
- Other unprofessional conduct

## Recognition

Contributors will be acknowledged in:
- Project README (for significant contributions)
- Release notes
- Individual recipe files (as appropriate)

## Questions?

- Open a GitHub Discussion for general questions
- Create an issue for specific problems
- Tag maintainers for urgent matters

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

Thank you for helping make this cookbook better! 🎉
