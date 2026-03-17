# React Patterns

## Component Composition
Prefer passing JSX as children over prop drilling.
```tsx
// Good
<Wrapper>
  <Header />
  <Content />
</Wrapper>

// Avoid
<Wrapper header={<Header />} content={<Content />} />
```

## Custom Hooks
Encapsulate complex logic or side effects.
```tsx
const { data, loading, error } = useFetchData('/api/resource');
```

## Context for Feature State
Use Context for feature-scoped state (e.g., a multi-step form), not global app state.

## Render Props (Rarely needed with Hooks)
Only use if absolute flexibility is required for a library component.

## Error Boundaries
Wrap critical sections in Error Boundaries to prevent full app crash.
