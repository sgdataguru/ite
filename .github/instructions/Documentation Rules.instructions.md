---
applyTo: '**'
---

# Documentation Rules

## Purpose
Ensure uniformity in technical documentation and automate the creation of accurate, up-to-date artifacts across the project. Good documentation saves time, reduces bugs, and improves onboarding.

---

## Quick Reference

| Element | Documentation Required | Priority |
|---------|----------------------|----------|
| Public API functions | JSDoc with params, returns, examples | High |
| React Components | Props, variants, usage examples | High |
| Custom Hooks | Parameters, return values, caveats | High |
| Types/Interfaces | Purpose, property descriptions | Medium |
| Complex algorithms | Step-by-step explanation | High |
| Environment variables | Purpose, format, required? | High |
| Utility functions | Purpose, examples | Medium |
| Internal helpers | Brief inline comment | Low |

---

## Core Principles

1. **Document WHY, not WHAT** - Code shows what; docs explain why decisions were made
2. **Keep docs close to code** - Update documentation when code changes
3. **Examples are essential** - Every public API needs usage examples
4. **Stay concise** - Prefer clarity over completeness
5. **Automate when possible** - Use tools to generate and validate docs

---

## JSDoc Standards

### Function Documentation

```typescript
/**
 * Short description of what the function does (imperative mood)
 * 
 * @description
 * Optional longer description explaining context, edge cases,
 * or implementation details not obvious from the code.
 * 
 * @param {Type} name - Parameter description
 * @param {Type} [optionalParam] - Optional parameter
 * @param {Type} [paramWithDefault='value'] - Parameter with default
 * @returns {ReturnType} Description of return value
 * @throws {ErrorType} When/why this error is thrown
 * 
 * @example
 * // Basic usage
 * const result = myFunction('input');
 * 
 * @example
 * // With options
 * const result = myFunction('input', { option: true });
 * 
 * @see {@link relatedFunction}
 * @deprecated Use {@link newFunction} instead. Will be removed in v3.0.
 */
```

### Component Documentation

```typescript
/**
 * Card component for displaying content in a contained area
 * 
 * @component
 * @category UI
 * 
 * @description
 * A flexible card component that supports headers, footers, and various
 * visual styles. Follows the LinkedIn design system with subtle shadows
 * and rounded corners.
 * 
 * @param {CardProps} props
 * @param {ReactNode} props.children - Card content
 * @param {string} [props.title] - Optional card header
 * @param {ReactNode} [props.footer] - Optional footer content
 * @param {'default'|'elevated'} [props.variant='default'] - Visual style
 * @param {boolean} [props.loading=false] - Show loading state
 * 
 * @returns {JSX.Element} Rendered card component
 * 
 * @example
 * // Basic card
 * <Card title="User Profile">
 *   <p>Content here</p>
 * </Card>
 * 
 * @example
 * // Elevated with footer
 * <Card 
 *   title="Settings" 
 *   variant="elevated"
 *   footer={<Button>Save</Button>}
 * >
 *   <SettingsForm />
 * </Card>
 * 
 * @accessibility
 * - Uses semantic HTML (article element)
 * - Loading state announces to screen readers
 * - Title renders as h3 if provided
 */
```

### Hook Documentation

```typescript
/**
 * Manages localStorage with automatic serialization
 * 
 * @description
 * Provides a stateful interface to localStorage that syncs across tabs.
 * Automatically JSON serializes/deserializes values. Handles SSR gracefully.
 * 
 * @param {string} key - localStorage key
 * @param {T} initialValue - Default value if key doesn't exist
 * @returns {[T, (value: T | ((prev: T) => T)) => void]} 
 *   Tuple of [storedValue, setValue]
 * 
 * @example
 * // Basic usage
 * const [theme, setTheme] = useLocalStorage('theme', 'light');
 * 
 * @example
 * // With complex objects
 * const [user, setUser] = useLocalStorage<User>('user', { id: null });
 * 
 * @caveats
 * - Values must be JSON serializable
 * - Maximum ~5MB storage limit
 * - Returns initialValue during SSR
 */
function useLocalStorage<T>(key: string, initialValue: T) { ... }
```

---

## Type Documentation

### Interface Documentation

```typescript
/**
 * Configuration options for API client
 * 
 * @interface ApiClientConfig
 * @category Types/Network
 * 
 * @property {string} baseUrl - API base URL (e.g., https://api.example.com/v1)
 * @property {number} [timeout=10000] - Request timeout in milliseconds
 * @property {number} [retries=3] - Number of retry attempts for failed requests
 * @property {RetryStrategy} [retryStrategy='exponential'] - Retry backoff strategy
 * @property {Record<string, string>} [headers] - Default headers for all requests
 * @property {(error: Error) => void} [onError] - Global error handler callback
 * 
 * @example
 * const config: ApiClientConfig = {
 *   baseUrl: 'https://api.example.com',
 *   timeout: 5000,
 *   retries: 2,
 *   headers: { 'X-API-Key': 'secret' }
 * };
 */
interface ApiClientConfig {
  baseUrl: string;
  timeout?: number;
  retries?: number;
  retryStrategy?: 'linear' | 'exponential';
  headers?: Record<string, string>;
  onError?: (error: Error) => void;
}
```

### Type Alias Documentation

```typescript
/**
 * Result type for operations that may fail
 * 
 * @description
 * Use this type for functions that need to return either success data
 * or error information. Forces callers to handle both cases.
 * 
 * @template T - Type of successful result data
 * @template E - Type of error (defaults to AppError)
 * 
 * @example
 * async function fetchUser(id: string): Promise<Result<User>> {
 *   try {
 *     const user = await db.users.findById(id);
 *     return { success: true, data: user };
 *   } catch (error) {
 *     return { success: false, error: toAppError(error) };
 *   }
 * }
 */
type Result<T, E = AppError> = 
  | { success: true; data: T }
  | { success: false; error: E };
```

### Enum Documentation

```typescript
/**
 * User account status lifecycle states
 * 
 * @enum {string} AccountStatus
 * @category Types/User
 * 
 * @description
 * Represents the complete lifecycle of a user account from creation
 * through potential suspension or deletion.
 */
enum AccountStatus {
  /** Account created but email not yet verified */
  PENDING_VERIFICATION = 'PENDING_VERIFICATION',
  /** Fully active account with all permissions */
  ACTIVE = 'ACTIVE',
  /** Temporarily disabled by user or admin */
  SUSPENDED = 'SUSPENDED',
  /** Permanently deleted (soft delete) */
  DELETED = 'DELETED',
}
```

---

## README Templates

### Project README

```markdown
# Project Name

> One-line description of what this project does

## Overview

2-3 sentences explaining the project's purpose, target users, and
key value proposition.

## Features

- ✨ **Feature One** - Brief description of benefit
- 🔒 **Feature Two** - Brief description of benefit
- 📊 **Feature Three** - Brief description of benefit

## Tech Stack

| Category | Technology |
|----------|------------|
| Framework | Next.js 15 (App Router) |
| Language | TypeScript 5.x |
| Styling | Tailwind CSS |
| UI Components | shadcn/ui |
| Database | PostgreSQL |
| Auth | NextAuth.js |

## Quick Start

### Prerequisites

- Node.js 20+
- pnpm 9+
- Docker (for local database)

### Installation

\`\`\`bash
# Clone repository
git clone https://github.com/org/repo.git
cd repo

# Install dependencies
pnpm install

# Set up environment
cp .env.example .env.local
# Edit .env.local with your values

# Start database
docker-compose up -d

# Run migrations
pnpm db:migrate

# Seed development data
pnpm db:seed

# Start development server
pnpm dev
\`\`\`

Visit [http://localhost:3000](http://localhost:3000)

### Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `DATABASE_URL` | PostgreSQL connection string | Yes |
| `NEXTAUTH_SECRET` | NextAuth secret (generate with `openssl rand -base64 32`) | Yes |
| `NEXTAUTH_URL` | App URL (http://localhost:3000 for dev) | Yes |

## Development

### Project Structure

\`\`\`
├── app/                 # Next.js App Router
│   ├── (auth)/         # Route groups
│   ├── api/            # API routes
│   └── layout.tsx      # Root layout
├── components/          # React components
│   ├── ui/             # shadcn/ui components
│   └── features/       # Feature-specific
├── hooks/               # Custom hooks
├── lib/                 # Utilities
│   ├── db/             # Database config
│   └── utils.ts        # Helper functions
├── services/            # API clients
├── types/               # TypeScript types
└── tests/               # Test files
\`\`\`

### Available Scripts

| Command | Description |
|---------|-------------|
| `pnpm dev` | Start dev server with Turbopack |
| `pnpm build` | Production build |
| `pnpm start` | Start production server |
| `pnpm lint` | ESLint check |
| `pnpm lint:fix` | ESLint with auto-fix |
| `pnpm type-check` | TypeScript compilation check |
| `pnpm test` | Run unit tests |
| `pnpm test:e2e` | Run E2E tests |
| `pnpm db:migrate` | Run database migrations |
| `pnpm db:generate` | Generate Prisma client |

### Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md) for development workflow.

## Documentation

- [Architecture](./docs/ARCHITECTURE.md)
- [API Reference](./docs/API.md)
- [Deployment](./docs/DEPLOYMENT.md)

## License

[MIT](./LICENSE)
```

### Component README (for complex components)

```markdown
# ComponentName

Brief description of the component's purpose and when to use it.

## Import

\`\`\`tsx
import { ComponentName } from '@/components/ui/ComponentName';
\`\`\`

## Usage

### Basic

\`\`\`tsx
<ComponentName 
  requiredProp="value"
  onAction={handleAction}
/>
\`\`\`

### Advanced

\`\`\`tsx
<ComponentName 
  requiredProp="value"
  optionalProp={42}
  variant="secondary"
  onAction={handleAction}
  renderCustom={(item) => <CustomItem item={item} />}
/>
\`\`\`

## Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `requiredProp` | `string` | — | **Required.** Description here |
| `optionalProp` | `number` | `0` | Description here |
| `variant` | `'primary' \| 'secondary'` | `'primary'` | Visual style variant |
| `onAction` | `(event: ActionEvent) => void` | — | Called when action occurs |
| `renderCustom` | `(item: Item) => ReactNode` | — | Custom render function |

## Examples

### With State Management

\`\`\`tsx
function Example() {
  const [value, setValue] = useState('');
  
  return (
    <ComponentName
      value={value}
      onChange={setValue}
    />
  );
}
\`\`\`

### Integration with Form Libraries

\`\`\`tsx
// With React Hook Form
<Controller
  name="field"
  control={control}
  render={({ field }) => (
    <ComponentName {...field} />
  )}
/>
\`\`\`

## Accessibility

- ✅ Keyboard navigable (Tab, Enter, Escape)
- ✅ Screen reader announcements for state changes
- ✅ ARIA labels on icon-only buttons
- ✅ Focus trap in modals
- ✅ Respects `prefers-reduced-motion`

## Testing

\`\`\`tsx
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';

it('should call onAction when clicked', async () => {
  const onAction = jest.fn();
  render(<ComponentName onAction={onAction} />);
  
  await userEvent.click(screen.getByRole('button'));
  expect(onAction).toHaveBeenCalled();
});
\`\`\`

## Related

- [RelatedComponent1](../RelatedComponent1)
- [Design System - Figma](https://figma.com/file/xxx)
```

---

## Inline Documentation

### Comment Conventions

```typescript
// ============================================
// SECTION: Section Name
// ============================================

/**
 * Block comment for:
 * - Complex algorithms
 * - Business logic explanations
 * - External references
 */

// Single-line comment for:
// - Brief clarifications
// - Implementation notes
// - Temporary workarounds

// TODO: Implement caching (issue #123)
// FIXME: Handle Safari flexbox bug (Safari < 16)
// NOTE: This value comes from the API as cents
// HACK: Workaround for third-party library limitation
// WARNING: This function is deprecated, use X instead
// REVIEW: Check performance with large datasets
```

### Complex Logic Documentation

```typescript
/**
 * Calculates optimal image sizes for responsive srcset
 * 
 * Algorithm:
 * 1. Determine layout width from container queries
 * 2. Calculate device pixel ratio (1x, 2x, 3x)
 * 3. Generate sizes: 320w, 640w, 960w, 1280w, 1920w
 * 4. Filter sizes larger than source image
 * 5. Add source width as max size
 * 
 * @see https://web.dev/optimize-lcp/#responsive-images
 */
function generateSrcset(image: ImageAsset): string {
  // Implementation...
}

// Alternative: Inline step comments
function calculateMetrics(data: DataPoint[]): Metrics {
  // Step 1: Filter out invalid data points
  const valid = data.filter(isValidDataPoint);
  
  // Step 2: Normalize to same time granularity (hourly)
  const normalized = normalizeToHourly(valid);
  
  // Step 3: Calculate rolling averages (24h window)
  const smoothed = calculateRollingAverage(normalized, 24);
  
  // Step 4: Extract key metrics
  return {
    average: calculateMean(smoothed),
    peak: Math.max(...smoothed),
    trend: calculateTrendLine(smoothed),
  };
}
```

### Magic Numbers

```typescript
// ❌ Avoid
if (retries > 3) { ... }

// ✅ Use named constants
/**
 * Maximum retry attempts before circuit breaker opens.
 * Based on p99 latency measurements showing 99.9% 
 * success within 3 attempts.
 */
const MAX_RETRY_ATTEMPTS = 3;

if (retries > MAX_RETRY_ATTEMPTS) { ... }
```

---

## API Documentation

### OpenAPI/Swagger Specification

Document all API endpoints using OpenAPI 3.0+:

```yaml
# openapi.yaml
openapi: 3.0.3
info:
  title: Project API
  version: 1.0.0
  description: |
    API documentation for the project.
    
    ## Authentication
    All endpoints require a Bearer token in the Authorization header:
    `Authorization: Bearer <token>`

paths:
  /users/{id}:
    get:
      summary: Get user by ID
      description: Returns detailed user information
      tags:
        - Users
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: string
          description: User's unique identifier
      responses:
        '200':
          description: User found
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
              example:
                id: "user_123"
                name: "John Doe"
                email: "john@example.com"
        '404':
          description: User not found
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Error'
              example:
                error:
                  code: "USER_NOT_FOUND"
                  message: "No user found with ID user_123"

components:
  schemas:
    User:
      type: object
      required:
        - id
        - name
        - email
      properties:
        id:
          type: string
          description: Unique identifier
        name:
          type: string
          description: Display name
        email:
          type: string
          format: email
        createdAt:
          type: string
          format: date-time
    
    Error:
      type: object
      required:
        - error
      properties:
        error:
          type: object
          properties:
            code:
              type: string
            message:
              type: string
```

### API Route Documentation (Next.js)

```typescript
/**
 * GET /api/users/:id
 * 
 * Retrieves a user by their ID. Returns 404 if user doesn't exist.
 * Requires authentication.
 * 
 * @route GET /api/users/:id
 * @authentication Required
 * 
 * @param {Object} params
 * @param {string} params.id - User ID
 * 
 * @returns {Promise<NextResponse>}
 * @returns {Object} 200 - User object
 * @returns {Object} 404 - User not found
 * @returns {Object} 401 - Unauthorized
 * 
 * @example
 * // Request
 * GET /api/users/user_123
 * Authorization: Bearer <token>
 * 
 * @example
 * // Response 200
 * {
 *   "id": "user_123",
 *   "name": "John Doe",
 *   "email": "john@example.com"
 * }
 */
export async function GET(
  request: Request,
  { params }: { params: { id: string } }
) {
  // Implementation
}
```

---

## Architecture Decision Records (ADRs)

Document significant architectural decisions:

```markdown
# ADR-001: Use Next.js App Router

## Status
Accepted

## Context
We needed to choose a routing strategy for our Next.js application. Options were:
- Pages Router (traditional)
- App Router (newer, with RSC support)

## Decision
We will use the App Router for all new features.

## Consequences

### Positive
- Server Components by default reduce client JS
- Simplified data fetching with async components
- Better layout composition

### Negative
- Learning curve for team
- Some third-party libraries not yet compatible
- Migration effort from existing Pages Router code

## Alternatives Considered

### Pages Router
- **Pros:** Stable, well-documented, extensive ecosystem
- **Cons:** No RSC support, more client-side JavaScript

## References
- [Next.js App Router Docs](https://nextjs.org/docs/app)
- [RFC: App Router](link)
```

Store ADRs in `docs/adr/` with format `ADR-XXX-title.md`.

---

## Changelog Standards

Follow [Keep a Changelog](https://keepachangelog.com/) format:

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- New feature X that does Y
- Support for Z

### Changed
- Improved performance of A by 50%
- Updated dependency B to v2.0

### Deprecated
- Feature C is deprecated, use D instead

### Removed
- Support for Node 16

### Fixed
- Bug where E would F incorrectly
- Memory leak in component G

### Security
- Updated H dependency to patch CVE-2025-XXXX

## [1.2.0] - 2025-01-15

### Added
- User authentication with OAuth providers
- Dark mode support

### Fixed
- Layout shift on mobile navigation
```

---

## Documentation Maintenance

### When to Update Docs

| Trigger | Action Required |
|---------|-----------------|
| New public API | Add JSDoc + README example |
| Changed function signature | Update JSDoc + Migration guide |
| New environment variable | Update README + .env.example |
| Breaking change | Update CHANGELOG + Migration guide |
| New dependency | Update README tech stack |
| Architecture change | Create ADR |
| Bug fix with workaround | Add comment + CHANGELOG |

### Documentation Review Checklist

Before submitting PR:

- [ ] All new public functions have JSDoc
- [ ] Complex logic has inline comments explaining WHY
- [ ] README reflects current setup process (test it!)
- [ ] CHANGELOG updated for user-facing changes
- [ ] Environment variables documented
- [ ] Breaking changes have migration instructions
- [ ] Type exports are documented
- [ ] Examples compile and work
- [ ] Links are not broken
- [ ] No TODO comments without issue references

---

## Markdown Standards

### Formatting

```markdown
# Top-level heading (one per file)

## Second-level heading

### Third-level heading

**Bold** for emphasis, *italic* for definitions or terms.

`inline code` for file names, variable names, short commands.

\`\`\`typescript
// Code blocks with language tag
const example = "code";
\`\`\`

> Blockquotes for important notes or callouts

| Tables | For | Structured |
|--------|-----|------------|
| data   | and | comparison |

- Use bullet lists for unordered items
- Keep items parallel in structure
1. Use numbered lists for sequential steps
2. Or when referring to items by number

[Links](https://example.com) use this format.
![Images](path/to/image.png) include alt text.
```

### Writing Style

- Use **imperative mood** for instructions ("Run the command", not "You should run")
- Use **sentence case** for headings ("Getting started", not "Getting Started")
- Be **concise** - remove words that don't add meaning
- Use **active voice** when possible
- **Code examples** should be complete and runnable

---

## Tooling

### TypeDoc Configuration

```json
{
  "entryPoints": ["./src"],
  "entryPointStrategy": "expand",
  "out": "./docs/api",
  "exclude": ["**/*.test.ts", "**/*.stories.tsx"],
  "excludePrivate": true,
  "excludeProtected": true,
  "plugin": ["typedoc-plugin-markdown"],
  "readme": "none",
  "gitRevision": "main"
}
```

### Markdownlint Configuration

```json
{
  "default": true,
  "MD013": { "line_length": 100 },
  "MD024": { "siblings_only": true },
  "MD033": false
}
```

---

## Quick Doc Template

Use this template for quick inline documentation:

```typescript
/**
 * [What it does in one sentence]
 * 
 * @param [name] - [What it is]
 * @returns [What you get back]
 * 
 * @example
 * [Short code example]
 */
```
