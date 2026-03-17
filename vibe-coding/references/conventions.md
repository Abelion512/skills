# Coding Conventions

## Structure
- Use **atomic design** or **feature-based** folder structure (`src/features/auth`, `src/components/ui`).
- Do NOT barrel export (`index.ts` files) unless necessary for library boundaries.

## TypeScript
- **Strict Mode:** Always enabled.
- **No `any`:** Use `unknown` or specific types/interfaces.
- **Props:** Use `interface ComponentProps` exported alongside component.
- **Naming:** PascalCase for components/interfaces, camelCase for functions/vars.

## React
- **Functional Components:** Always.
- **Hooks:** Custom hooks for logic > 10 lines or reusable logic.
- **State:** Keep state local unless shared across unrelated components.
- **Effect:** Minimize `useEffect`. Prefer event handlers or derived state.

## Styling (Tailwind)
- Use utility classes first.
- Extract components only when repeated > 3 times.
- Use `cn()` helper for conditional classes.
