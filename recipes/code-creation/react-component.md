# React Component Creation Recipe

## Description
Build modern, reusable React components with proper TypeScript types, hooks, and accessibility.

## Prompt Template

```
Create a React component for [COMPONENT_PURPOSE] with the following requirements:
- Component type: [Functional component with hooks]
- Props interface: [SPECIFY_PROPS]
- State management: [useState/useReducer/Context]
- Styling approach: [CSS Modules/Styled Components/Tailwind]
- Include TypeScript types
- Include prop validation
- Include accessibility (ARIA) attributes
- Include error boundaries if applicable
- Follow React best practices (memo, useCallback, etc.)
- Include JSDoc comments
```

## Example Usage

### Example 1: Data Table Component

**Prompt:**
```
Create a React component for a sortable data table with the following requirements:
- Component type: Functional component with hooks
- Props interface: { data: Array<Record<string, any>>, columns: Array<{key: string, label: string, sortable?: boolean}>, onRowClick?: (row) => void }
- State management: useState for sort column and direction
- Styling approach: Tailwind CSS
- Include TypeScript types
- Include prop validation
- Include accessibility (ARIA) attributes for table, sorting buttons
- Follow React best practices (memo for performance, useCallback)
- Include JSDoc comments
- Support pagination with page size of 10
```

**Expected Output:**
- TypeScript component file
- Proper type definitions
- Sorting logic implementation
- Accessible table markup
- Performance optimizations

### Example 2: Form Input Component

**Prompt:**
```
Create a React component for a reusable form input field with the following requirements:
- Component type: Functional component with hooks
- Props interface: { label: string, type: string, value: string, onChange: (value: string) => void, error?: string, placeholder?: string, required?: boolean }
- State management: useState for focus state
- Styling approach: CSS Modules
- Include TypeScript types
- Include prop validation
- Include accessibility (ARIA) attributes for labels, errors, required fields
- Include error boundaries if applicable
- Follow React best practices
- Include JSDoc comments
- Support different input types (text, email, password, number)
```

## Best Practices

1. **TypeScript First**: Always request TypeScript for type safety
2. **Accessibility**: Include ARIA attributes and keyboard navigation
3. **Performance**: Request memo, useCallback, useMemo where appropriate
4. **Reusability**: Design for component reuse
5. **Testing**: Components should be easily testable
6. **Documentation**: Include JSDoc for props and component purpose

## Testing

Use [React Testing recipes](../testing/react-testing.md) to create component tests.

## Related Recipes

- [Component Optimization](../code-optimization/react-performance.md)
- [React Testing](../testing/react-testing.md)
- [Accessibility](../security/accessibility.md)
