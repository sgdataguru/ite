---
applyTo: '**'
---

# Code Quality Standards

## Purpose
Establish consistent coding practices and quality standards to ensure maintainable, readable, reliable, and secure code across the project.

---

## Quick Reference

| Category | Key Rule |
|----------|----------|
| **Types** | No `any` - use `unknown` + type guards |
| **Components** | Default to Server Components |
| **Naming** | PascalCase components, camelCase functions |
| **Imports** | External → Internal → Types → Relative |
| **Errors** | Always handle errors with typed results |
| **Testing** | Test behavior, not implementation |
| **A11y** | All interactive elements keyboard accessible |

---

## TypeScript Standards

### Type Safety (Strict Mode)

**Explicit Types Required**
```typescript
// ✅ Always define explicit return types for exported functions
export async function fetchUser(id: string): Promise<User> {
  const response = await fetch(`/api/users/${id}`);
  return response.json();
}

// ✅ Interface for all component props
interface ButtonProps {
  label: string;
  variant?: 'primary' | 'secondary' | 'tertiary';
  onClick?: () => void;
  disabled?: boolean;
  type?: 'button' | 'submit' | 'reset';
}

// ❌ NEVER use 'any' - disable with @typescript-eslint/no-explicit-any
function processData(data: any) { ... }

// ✅ Use 'unknown' with type guards
function processData(data: unknown): asserts data is ValidData {
  if (!isValidData(data)) {
    throw new Error('Invalid data structure');
  }
}
```

**Strict Null Checks**
```typescript
// ✅ Handle null/undefined explicitly
function getUserName(user: User | null): string {
  if (!user) return 'Anonymous';
  return user.name;
}

// ✅ Non-null assertion only when certain
const element = document.getElementById('app')!; // Only if checked before

// ✅ Optional chaining for nested access
const city = user?.address?.city ?? 'Unknown';
```

**Utility Types**
```typescript
// Use built-in utility types appropriately
type UserInput = Partial<Pick<User, 'name' | 'email'>>;
type UserPreview = Omit<User, 'password' | 'internalNotes'>;
type ReadonlyConfig = Readonly<Config>;

// ✅ Custom utility types for common patterns
type Nullable<T> = T | null;
type AsyncResult<T> = Promise<{ success: true; data: T } | { success: false; error: AppError }>;
```

### Type Guards & Narrowing

```typescript
// ✅ Use type predicates for custom guards
function isUser(obj: unknown): obj is User {
  return (
    typeof obj === 'object' &&
    obj !== null &&
    'id' in obj &&
    'email' in obj &&
    typeof (obj as User).id === 'string'
  );
}

// ✅ Discriminated unions for complex state
type AsyncState<T> =
  | { status: 'idle' }
  | { status: 'loading' }
  | { status: 'success'; data: T }
  | { status: 'error'; error: Error };

// Usage with exhaustive checks
function handleState<T>(state: AsyncState<T>) {
  switch (state.status) {
    case 'idle': return 'Waiting...';
    case 'loading': return 'Loading...';
    case 'success': return state.data;
    case 'error': return state.error.message;
    default: return assertNever(state); // Compile-time exhaustiveness check
  }
}
```

---

## React & Next.js Standards

### Component Architecture

**Server Components (Default)**
```typescript
// ✅ Server Component - No 'use client' directive
// Benefits: Zero JS bundle, direct DB access, secure
import { db } from '@/lib/db';

export default async function UserList() {
  const users = await db.users.findMany(); // Direct data access
  
  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

**Client Components (When Necessary)**
```typescript
// ✅ Client Component - Must have 'use client' directive
'use client';

import { useState, useCallback } from 'react';

interface CounterProps {
  initialCount?: number;
  onChange?: (count: number) => void;
}

export default function Counter({ initialCount = 0, onChange }: CounterProps) {
  const [count, setCount] = useState(initialCount);
  
  const increment = useCallback(() => {
    const newCount = count + 1;
    setCount(newCount);
    onChange?.(newCount);
  }, [count, onChange]);
  
  return (
    <button onClick={increment} type="button">
      Count: {count}
    </button>
  );
}
```

**Component Structure Pattern**
```typescript
// 1. Imports
import { useState, useCallback, memo } from 'react';
import { cn } from '@/lib/utils';

// 2. Types
interface UserCardProps {
  user: User;
  onSelect?: (user: User) => void;
  className?: string;
}

// 3. Constants
const AVATAR_SIZES = { sm: 32, md: 48, lg: 64 } as const;

// 4. Helper functions (if specific to component)
function getInitials(name: string): string {
  return name.split(' ').map(n => n[0]).join('').toUpperCase();
}

// 5. Component
export const UserCard = memo(function UserCard({ 
  user, 
  onSelect, 
  className 
}: UserCardProps) {
  // Hooks first
  const [isHovered, setIsHovered] = useState(false);
  
  // Derived state
  const initials = getInitials(user.name);
  const hasPremium = user.subscription === 'premium';
  
  // Event handlers
  const handleClick = useCallback(() => {
    onSelect?.(user);
  }, [onSelect, user]);
  
  // Early returns for edge cases
  if (!user.id) return null;
  
  // Render
  return (
    <div 
      className={cn('user-card', className)}
      onClick={handleClick}
      onMouseEnter={() => setIsHovered(true)}
      onMouseLeave={() => setIsHovered(false)}
    >
      {/* Content */}
    </div>
  );
});
```

### Modern React Patterns

**Server Actions**
```typescript
// ✅ Server Action for form submissions/mutations
'use server';

import { revalidatePath } from 'next/cache';
import { z } from 'zod';

const updateProfileSchema = z.object({
  name: z.string().min(1).max(100),
  bio: z.string().max(500).optional(),
});

export async function updateProfile(formData: FormData) {
  // Validate
  const result = updateProfileSchema.safeParse({
    name: formData.get('name'),
    bio: formData.get('bio'),
  });
  
  if (!result.success) {
    return { success: false, errors: result.error.flatten() };
  }
  
  // Execute
  try {
    await db.users.update({
      where: { id: userId },
      data: result.data,
    });
    
    revalidatePath('/profile');
    return { success: true };
  } catch (error) {
    return { success: false, error: 'Failed to update profile' };
  }
}
```

**Parallel Data Fetching**
```typescript
// ✅ Fetch in parallel when independent
export default async function Dashboard() {
  const [user, posts, notifications] = await Promise.all([
    getUser(),
    getPosts(),
    getNotifications(),
  ]);
  
  return <DashboardUI user={user} posts={posts} notifications={notifications} />;
}

// ✅ Use Suspense boundaries for progressive loading
import { Suspense } from 'react';

export default function Page() {
  return (
    <>
      <h1>Dashboard</h1>
      <Suspense fallback={<UserSkeleton />}>
        <UserProfile />
      </Suspense>
      <Suspense fallback={<PostsSkeleton />}>
        <PostsList />
      </Suspense>
    </>
  );
}
```

### Hooks Best Practices

**useState**
```typescript
// ✅ Type complex state
const [user, setUser] = useState<User | null>(null);
const [items, setItems] = useState<Item[]>([]);

// ✅ Functional updates for derived state
setCount(prev => prev + 1);

// ✅ Lazy initialization for expensive computations
const [data] = useState(() => expensiveComputation());
```

**useEffect**
```typescript
// ✅ Proper effect pattern with cleanup
useEffect(() => {
  let cancelled = false;
  const controller = new AbortController();
  
  async function loadData() {
    try {
      const data = await fetchData({ signal: controller.signal });
      if (!cancelled) {
        setData(data);
      }
    } catch (error) {
      if (!cancelled && error.name !== 'AbortError') {
        setError(error);
      }
    }
  }
  
  loadData();
  
  return () => {
    cancelled = true;
    controller.abort();
  };
}, [dependency]); // ✅ Complete, accurate dependency array

// ❌ Never ignore dependency warnings - fix or use eslint-disable with explanation
```

**Custom Hooks**
```typescript
// ✅ Prefix with 'use', single responsibility
function useLocalStorage<T>(key: string, initialValue: T) {
  const [value, setValue] = useState<T>(() => {
    if (typeof window === 'undefined') return initialValue;
    try {
      return JSON.parse(localStorage.getItem(key) ?? '') ?? initialValue;
    } catch {
      return initialValue;
    }
  });
  
  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);
  
  return [value, setValue] as const;
}

// ✅ Return typed, documented object for complex hooks
function useAsync<T>(asyncFn: () => Promise<T>) {
  const [state, setState] = useState<{
    data: T | null;
    loading: boolean;
    error: Error | null;
  }>({ data: null, loading: true, error: null });
  
  // Implementation...
  
  return state;
}
```

### Performance Optimization

```typescript
// ✅ Memoize expensive calculations
const sortedItems = useMemo(() => {
  return items.sort((a, b) => a.name.localeCompare(b.name));
}, [items]);

// ✅ Memoize callbacks passed to optimized children
const handleSubmit = useCallback((data: FormData) => {
  submitForm(data);
}, [submitForm]);

// ✅ Use React.memo for pure components that re-render often
const ListItem = memo(function ListItem({ item, onSelect }: ItemProps) {
  return <div onClick={() => onSelect(item)}>{item.name}</div>;
});

// ✅ Code splitting with dynamic imports
const HeavyChart = dynamic(() => import('./HeavyChart'), {
  loading: () => <ChartSkeleton />,
  ssr: false, // Disable SSR if component uses browser APIs
});
```

---

## Code Style Guidelines

### Naming Conventions

| Element | Convention | Example | ✅/❌ |
|---------|------------|---------|-------|
| React Components | PascalCase | `UserProfile`, `DashboardLayout` | ✅ |
| Functions | camelCase | `getUserById`, `formatDate` | ✅ |
| Variables | camelCase | `userName`, `isLoading` | ✅ |
| Constants | UPPER_SNAKE_CASE | `MAX_RETRIES`, `API_BASE_URL` | ✅ |
| Types/Interfaces | PascalCase | `User`, `ApiResponse` | ✅ |
| Enums | PascalCase | `UserRole`, `PaymentStatus` | ✅ |
| Files (components) | PascalCase | `UserProfile.tsx` | ✅ |
| Files (utilities) | camelCase | `formatDate.ts` | ✅ |
| Files (constants) | UPPER_SNAKE_CASE | `CONFIG.ts` | ✅ |
| CSS classes | kebab-case | `user-profile`, `nav-item` | ✅ |
| Boolean variables | is/has/can prefix | `isVisible`, `hasPermission` | ✅ |
| Event handlers | handle prefix | `handleClick`, `handleSubmit` | ✅ |

### Boolean Naming

```typescript
// ✅ Use semantic prefixes
const isLoading = true;
const hasError = error !== null;
const canSubmit = !isLoading && isValid;
const shouldRefetch = staleTime < Date.now();

// ❌ Avoid vague names
const loading = true;        // ❌
const error = true;          // ❌
const ok = true;             // ❌
```

### Function Naming

```typescript
// ✅ Action + Subject pattern
function fetchUser() { }
function createOrder() { }
function updateProfile() { }
function deleteItem() { }
function validateEmail() { }

// ✅ Transform pattern (Subject + Action)
function userToDTO(user: User) { }
function formatCurrency(amount: number) { }
function parseJSON<T>(json: string) { }

// ✅ Boolean checks
function isValidEmail(email: string) { }
function hasPermission(user: User, action: string) { }
function canAccess(user: User, resource: string) { }
```

---

## Error Handling

### Result Type Pattern

```typescript
// ✅ Standardized result type
type Result<T, E = AppError> = 
  | { success: true; data: T }
  | { success: false; error: E };

interface AppError {
  code: string;
  message: string;
  details?: Record<string, unknown>;
}

// Usage
async function fetchUser(id: string): Promise<Result<User>> {
  try {
    const response = await fetch(`/api/users/${id}`);
    
    if (!response.ok) {
      return {
        success: false,
        error: {
          code: `HTTP_${response.status}`,
          message: response.statusText,
        },
      };
    }
    
    const data = await response.json();
    return { success: true, data };
  } catch (error) {
    return {
      success: false,
      error: {
        code: 'NETWORK_ERROR',
        message: error instanceof Error ? error.message : 'Unknown error',
      },
    };
  }
}

// Consumer
const result = await fetchUser('123');
if (result.success) {
  console.log(result.data.name);
} else {
  console.error(result.error.message);
}
```

### Error Boundaries

```typescript
'use client';

import { Component, type ReactNode } from 'react';

interface Props {
  children: ReactNode;
  fallback?: ReactNode;
  onError?: (error: Error, info: React.ErrorInfo) => void;
}

interface State {
  hasError: boolean;
  error?: Error;
}

export class ErrorBoundary extends Component<Props, State> {
  state: State = { hasError: false };

  static getDerivedStateFromError(error: Error): State {
    return { hasError: true, error };
  }

  componentDidCatch(error: Error, info: React.ErrorInfo) {
    this.props.onError?.(error, info);
    // Send to error reporting service
    console.error('ErrorBoundary caught:', error, info);
  }

  render() {
    if (this.state.hasError) {
      return this.props.fallback ?? (
        <div role="alert" className="error-fallback">
          <h2>Something went wrong</h2>
          <button onClick={() => this.setState({ hasError: false })}>
            Try again
          </button>
        </div>
      );
    }
    return this.props.children;
  }
}
```

---

## Accessibility (a11y) Standards

### Required Practices

```typescript
// ✅ Semantic HTML
<button onClick={handleClick}>Submit</button>
// ❌ <div onClick={handleClick}>Submit</div>

// ✅ ARIA labels for icon buttons
<button aria-label="Close dialog" onClick={onClose}>
  <XIcon />
</button>

// ✅ Form labels
<label htmlFor="email">Email</label>
<input id="email" type="email" aria-required="true" />

// ✅ Error associations
<input 
  id="email" 
  aria-invalid={hasError}
  aria-describedby={hasError ? 'email-error' : undefined}
/>
{hasError && <span id="email-error" role="alert">{error}</span>}

// ✅ Keyboard navigation
<div role="dialog" aria-modal="true" aria-labelledby="dialog-title">
  <h2 id="dialog-title">Confirm Action</h2>
  {/* Trap focus inside modal */}
</div>

// ✅ Skip links for keyboard users
<a href="#main-content" className="skip-link">Skip to main content</a>
<main id="main-content">...</main>

// ✅ Focus management
const buttonRef = useRef<HTMLButtonElement>(null);
useEffect(() => {
  if (isOpen) {
    buttonRef.current?.focus();
  }
}, [isOpen]);
```

### Accessibility Checklist

- [ ] All images have meaningful `alt` text (empty for decorative)
- [ ] Color contrast ratio ≥ 4.5:1 for normal text, 3:1 for large text
- [ ] All interactive elements are keyboard accessible
- [ ] Focus order is logical and visible
- [ ] Form inputs have associated labels
- [ ] Error messages are announced to screen readers
- [ ] Animations respect `prefers-reduced-motion`

---

## Security Best Practices

### Input Handling

```typescript
// ✅ Always validate and sanitize input
import { z } from 'zod';

const userSchema = z.object({
  email: z.string().email(),
  name: z.string().min(1).max(100),
});

// Validate on server
export async function createUser(formData: FormData) {
  const result = userSchema.safeParse({
    email: formData.get('email'),
    name: formData.get('name'),
  });
  
  if (!result.success) {
    return { error: 'Invalid input' };
  }
  
  // Proceed with validated data
}

// ✅ Sanitize HTML if rendering user content
import DOMPurify from 'isomorphic-dompurify';

function UserContent({ html }: { html: string }) {
  const clean = DOMPurify.sanitize(html);
  return <div dangerouslySetInnerHTML={{ __html: clean }} />;
}
```

### Environment Variables

```typescript
// ✅ Never expose secrets to client
// .env.local
DATABASE_URL=postgresql://...        // ✅ Server-only
NEXT_PUBLIC_API_URL=https://api.com  // ✅ Public - safe for client
SECRET_KEY=abc123                    // ✅ Server-only

// Access patterns
const dbUrl = process.env.DATABASE_URL;                    // Server
const apiUrl = process.env.NEXT_PUBLIC_API_URL;            // Client + Server
// const secret = process.env.SECRET_KEY;                  // ❌ Never in client code
```

### Authentication Checks

```typescript
// ✅ Always verify auth on server
import { auth } from '@clerk/nextjs/server';

export default async function AdminPage() {
  const { userId } = await auth();
  
  if (!userId) {
    redirect('/sign-in');
  }
  
  const user = await getUser(userId);
  
  if (user.role !== 'admin') {
    redirect('/unauthorized');
  }
  
  return <AdminDashboard />;
}
```

---

## Code Organization

### Import Order

```typescript
// 1. React/Next.js imports
import { useState, useEffect, Suspense } from 'react';
import { notFound } from 'next/navigation';
import Image from 'next/image';

// 2. Third-party libraries
import { clsx, type ClassValue } from 'clsx';
import { twMerge } from 'tailwind-merge';
import { z } from 'zod';

// 3. Internal absolute imports
import { Button } from '@/components/ui/Button';
import { useAuth } from '@/hooks/useAuth';
import { cn } from '@/lib/utils';

// 4. Types (use 'import type')
import type { User, Post } from '@/types';

// 5. Relative imports
import { PostCard } from './PostCard';
import styles from './page.module.css';
```

### File Structure

```
my-component/
├── index.ts              # Public API exports
├── MyComponent.tsx       # Main component
├── MyComponent.test.tsx  # Tests
├── MyComponent.module.css # Styles (if not using Tailwind)
├── types.ts              # Component-specific types
├── constants.ts          # Component constants
└── utils.ts              # Component-specific utilities
```

---

## Comments & Documentation

### Comment Guidelines

```typescript
// ✅ Explain WHY, not WHAT
// Debounce search to avoid excessive API calls
const debouncedSearch = useMemo(() => debounce(search, 300), [search]);

// ✅ Document complex business logic
// Premium access is granted if ANY of:
// 1. Active subscription
// 2. Within 14-day trial period
// 3. Grandfathered from legacy plan
const hasPremium = 
  subscription?.status === 'active' ||
  (trialStart && Date.now() - trialStart < 14 * 24 * 60 * 60 * 1000) ||
  isLegacyUser;

// ❌ Obvious comments
// Increment counter
setCount(c => c + 1);

// ✅ TODO format
// TODO: Implement pagination for datasets > 1000 rows
// TODO(@username): Remove after API v2 migration (due: 2024-03-01)
// FIXME: Handle Safari 14 flexbox bug
// HACK: Workaround for third-party library limitation
```

### JSDoc for Public APIs

```typescript
/**
 * Formats a number as localized currency string.
 * 
 * @param amount - Numeric amount to format
 * @param currency - ISO 4217 currency code (default: 'USD')
 * @param locale - BCP 47 locale identifier (default: 'en-US')
 * @returns Formatted currency string
 * @throws {RangeError} If currency code is invalid
 * 
 * @example
 * formatCurrency(1234.56) // '$1,234.56'
 * formatCurrency(1234.56, 'EUR', 'de-DE') // '1.234,56 €'
 */
export function formatCurrency(
  amount: number,
  currency = 'USD',
  locale = 'en-US'
): string {
  return new Intl.NumberFormat(locale, {
    style: 'currency',
    currency,
  }).format(amount);
}
```

---

## Testing Standards

### Test Structure (AAA Pattern)

```typescript
import { render, screen, fireEvent } from '@testing-library/react';
import { UserCard } from './UserCard';

describe('UserCard', () => {
  const mockUser = { id: '1', name: 'John Doe', email: 'john@example.com' };
  
  describe('rendering', () => {
    it('should display user name and email', () => {
      // Arrange
      render(<UserCard user={mockUser} />);
      
      // Act (nothing needed for render tests)
      
      // Assert
      expect(screen.getByText('John Doe')).toBeInTheDocument();
      expect(screen.getByText('john@example.com')).toBeInTheDocument();
    });
    
    it('should show placeholder when user has no avatar', () => {
      render(<UserCard user={{ ...mockUser, avatar: null }} />);
      
      expect(screen.getByTestId('avatar-placeholder')).toBeInTheDocument();
    });
  });
  
  describe('interactions', () => {
    it('should call onSelect when clicked', () => {
      const onSelect = jest.fn();
      render(<UserCard user={mockUser} onSelect={onSelect} />);
      
      fireEvent.click(screen.getByRole('button'));
      
      expect(onSelect).toHaveBeenCalledWith(mockUser);
    });
  });
  
  describe('accessibility', () => {
    it('should be keyboard accessible', () => {
      render(<UserCard user={mockUser} />);
      
      const card = screen.getByRole('button');
      expect(card).toHaveAttribute('tabIndex', '0');
    });
  });
});
```

### Testing Best Practices

```typescript
// ✅ Test behavior, not implementation
// ❌ expect(component.instance().state.isOpen).toBe(true)
// ✅ expect(screen.getByText('Content')).toBeVisible()

// ✅ Use userEvent over fireEvent for realistic interactions
import userEvent from '@testing-library/user-event';

const user = userEvent.setup();
await user.click(screen.getByRole('button'));
await user.type(screen.getByLabelText('Email'), 'test@example.com');

// ✅ Test loading and error states
it('should show loading state', () => {
  render(<AsyncComponent />);
  expect(screen.getByRole('status')).toHaveTextContent('Loading...');
});

it('should show error message on failure', async () => {
  server.use(http.get('/api/data', () => HttpResponse.error()));
  render(<AsyncComponent />);
  
  await waitFor(() => {
    expect(screen.getByRole('alert')).toHaveTextContent(/error/i);
  });
});
```

---

## Git Standards

### Commit Message Format (Conventional Commits)

```
<type>(<scope>): <subject>

[optional body]

[optional footer(s)]
```

**Types:**
| Type | Use When |
|------|----------|
| `feat` | New feature |
| `fix` | Bug fix |
| `docs` | Documentation only |
| `style` | Code formatting (no logic change) |
| `refactor` | Code restructuring |
| `perf` | Performance improvement |
| `test` | Adding/updating tests |
| `chore` | Build, dependencies, config |
| `ci` | CI/CD changes |

**Examples:**
```bash
feat(auth): add OAuth with Google provider

fix(dashboard): resolve data fetching on mobile safari
- Added polyfill for fetch API
- Fixed layout overflow issue

refactor(api): extract validation to shared module

BREAKING CHANGE: validation functions now return Result type
```

### Branch Naming

```
feature/user-authentication
bugfix/login-redirect-loop
refactor/dashboard-components
docs/api-examples
hotfix/security-patch
```

---

## Pre-commit & CI

### ESLint Configuration

```javascript
// eslint.config.mjs
export default [
  {
    rules: {
      '@typescript-eslint/no-explicit-any': 'error',
      '@typescript-eslint/explicit-function-return-type': 'warn',
      'no-console': ['warn', { allow: ['error', 'warn'] }],
      'react-hooks/exhaustive-deps': 'error',
    },
  },
];
```

### Pre-commit Checklist

```bash
# Run before every commit
pnpm lint          # ESLint + Prettier
pnpm type-check    # TypeScript compilation
pnpm test          # Unit tests
pnpm build         # Production build
```

---

## Code Review Checklist

### Before Submitting PR

- [ ] Code compiles without errors or warnings
- [ ] All TypeScript strict checks pass (`noImplicitAny`, `strictNullChecks`)
- [ ] All tests pass with good coverage
- [ ] No `console.log` or `debugger` statements
- [ ] No `any` types (document exceptions with `eslint-disable`)
- [ ] Proper error handling with typed results
- [ ] Loading and error states in UI
- [ ] Accessibility: keyboard navigation, ARIA labels, focus management
- [ ] No hardcoded values (use constants/environment variables)
- [ ] Security: input validation, no secrets exposed
- [ ] Performance: memoization where needed, no unnecessary re-renders
- [ ] Comments explain WHY, not WHAT
- [ ] Follows naming conventions throughout
- [ ] Commit messages follow conventional format

### Reviewer Checklist

- [ ] Code is readable and maintainable
- [ ] Architecture patterns are followed
- [ ] Edge cases are handled
- [ ] Tests cover critical paths
- [ ] Documentation is updated
- [ ] Breaking changes are documented

---

## Common Pitfalls to Avoid

```typescript
// ❌ Prop drilling - use composition or context
// ❌ useEffect for derived state - use useMemo
// ❌ Inline objects/arrays in deps - useMemo/useCallback
// ❌ Index as key in lists - use stable IDs
// ❌ Mutating state directly - always return new objects
// ❌ async useEffect without cleanup - use AbortController
// ❌ Missing error boundaries - wrap route sections
// ❌ Large client bundles - use Server Components by default
```
