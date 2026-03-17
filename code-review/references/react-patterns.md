# React + TypeScript Patterns Reference

> Loaded as context for code-review skill. React 19 + TypeScript 5.

## Component Patterns

### Compound Components
```typescript
interface CardProps { children: React.ReactNode }
interface CardHeaderProps { title: string; subtitle?: string }

function Card({ children }: CardProps) {
  return <div className="rounded-2xl border p-4">{children}</div>
}
function CardHeader({ title, subtitle }: CardHeaderProps) {
  return <div><h3>{title}</h3>{subtitle && <p>{subtitle}</p>}</div>
}
Card.Header = CardHeader
export { Card }
```

### Custom Hook Pattern
```typescript
// ✅ Encapsulate logic in hooks
function useUserProfile(userId: string) {
  const { data, isLoading, error } = useQuery({
    queryKey: ['user', userId],
    queryFn: () => fetchUser(userId),
  })
  return { user: data, isLoading, error }
}
```

### Render Props / Slot Pattern (shadcn style)
```typescript
interface DialogProps {
  trigger: React.ReactNode
  children: React.ReactNode
}
```

## React 19 Patterns

### useTransition for non-urgent updates
```typescript
const [isPending, startTransition] = useTransition()

function handleSearch(query: string) {
  startTransition(() => {
    setSearchResults(performSearch(query))
  })
}
```

### useOptimistic for optimistic UI
```typescript
const [optimisticLikes, addOptimisticLike] = useOptimistic(
  likes,
  (state, newLike: Like) => [...state, newLike]
)
```

### Server Actions (if using Next.js)
```typescript
'use server'
async function createPost(formData: FormData) {
  const title = formData.get('title') as string
  const { error } = await supabase.from('posts').insert({ title })
  if (error) throw new Error(error.message)
  revalidatePath('/posts')
}
```

## TypeScript Patterns

### Discriminated Unions
```typescript
type RequestState<T> =
  | { status: 'idle' }
  | { status: 'loading' }
  | { status: 'success'; data: T }
  | { status: 'error'; error: string }
```

### Zod + TypeScript
```typescript
const UserSchema = z.object({
  id: z.string().uuid(),
  email: z.string().email(),
  role: z.enum(['admin', 'user']),
})
type User = z.infer<typeof UserSchema>
```

## Common Anti-Patterns to Flag

```typescript
// ❌ useEffect with missing deps
useEffect(() => {
  fetchData(userId) // userId not in deps
}, [])

// ✅ Correct
useEffect(() => {
  fetchData(userId)
}, [userId])

// ❌ Direct state mutation
const handleAdd = () => {
  items.push(newItem) // mutates state directly
  setItems(items)
}

// ✅ Immutable update
const handleAdd = () => {
  setItems(prev => [...prev, newItem])
}

// ❌ Index as key
items.map((item, index) => <Item key={index} {...item} />)

// ✅ Stable unique key
items.map((item) => <Item key={item.id} {...item} />)
```
