# Code Review Checklist

## Functionality
- [ ] Does the code do what it's supposed to do?
- [ ] Are edge cases handled?
- [ ] Does it break existing features?

## Code Quality
- [ ] No `any` types used.
- [ ] Variable and function names are descriptive.
- [ ] Code is DRY (Don't Repeat Yourself).
- [ ] No console.log or dead code committed.
- [ ] Functions are short and single-responsibility.

## Performance
- [ ] No unnecessary re-renders (check `useEffect` dependencies).
- [ ] Are expensive calculations memoized (`useMemo`)?
- [ ] Are list items keyed properly?

## Security
- [ ] No secrets in code.
- [ ] User input sanitized.
- [ ] RLS policies checked for new tables.

## Testing
- [ ] Are critical paths tested?
- [ ] Do existing tests pass?
