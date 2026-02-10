---
applyTo: '**'
---

# Architecture & Design Guidelines

## Purpose
Standardize system design patterns and technical structures while ensuring compliance with architectural principles and security protocols.

---

## Design Inspiration: LinkedIn Professional Network Aesthetic

*Inspired by LinkedIn (https://linkedin.com) and professional networking platforms*

### Branding & Logo

- Use LinkedIn's professional aesthetic for all public-facing assets
- Primary logo source: LinkedIn wordmark and "in" bug logo
- Logo usage: Use LinkedIn blue (#0A66C2) on light backgrounds; white/negative variant on dark backgrounds
- Clearspace: maintain at least 16px of clear space around the logo on UI elements
- Do not alter the logo proportions, colors, or add effects that obscure legibility

Add brand assets (SVGs, color tokens) to the `public/brand/` folder and reference them from components as `/brand/linkedin-logo.svg`.

### Color Palette

**Primary Colors (LinkedIn)**
```css
--linkedin-blue: #0A66C2;            /* LinkedIn Blue - trust, professionalism */
--linkedin-blue-dark: #004182;       /* Dark blue - emphasis, hover states */
--linkedin-blue-light: #E2F0FE;      /* Light blue - backgrounds, highlights */
--linkedin-blue-hover: #004182;      /* Hover state blue */
```

**Secondary Colors**
```css
--color-teal: #378FE9;               /* Teal - interactive elements */
--color-green: #057642;              /* Green - success, growth, positive actions */
--color-green-light: #E6F4EA;        /* Light green - success backgrounds */
--color-amber: #B24020;              /* Amber/copper - warmth, premium */
--color-purple: #8C68CB;             /* Purple - premium features */
```

**Neutral Colors**
```css
--color-black: #000000;              /* Pure black - emphasis */
--color-white: #FFFFFF;              /* White - backgrounds */
--color-gray-900: #1D1D1D;           /* Near black - primary text */
--color-gray-800: #333333;           /* Dark gray - secondary text */
--color-gray-700: #5E5E5E;           /* Medium gray - tertiary text */
--color-gray-600: #7A7A7A;           /* Gray - muted text */
--color-gray-400: #9E9E9E;           /* Light gray - placeholders */
--color-gray-300: #C5C5C5;           /* Lighter gray - borders */
--color-gray-200: #E0E0E0;           /* Very light gray - dividers */
--color-gray-100: #F3F2EF;           /* LinkedIn background gray */
--color-gray-50: #F9FAFB;            /* Lightest gray - subtle backgrounds */
```

**Background & Surface**
```css
--bg-primary: #F3F2EF;               /* LinkedIn signature background */
--bg-secondary: #FFFFFF;             /* Card/content backgrounds */
--bg-dark: #1D1D1D;                  /* Dark sections */
--bg-card: #FFFFFF;                  /* Card backgrounds */
--bg-overlay: rgba(0, 0, 0, 0.75);   /* Modal overlays */
--bg-hover: rgba(0, 0, 0, 0.05);     /* Subtle hover state */
```

**Text Colors**
```css
--text-primary: #1D1D1D;             /* Primary text - high contrast */
--text-secondary: #5E5E5E;           /* Secondary text */
--text-tertiary: #7A7A7A;            /* Tertiary/muted text */
--text-light: #FFFFFF;               /* White text on dark */
--text-accent: #0A66C2;              /* LinkedIn blue - links */
--text-link-hover: #004182;          /* Link hover state */
```

**Semantic Colors**
```css
--success: #057642;                  /* Green - success, growth */
--success-light: #E6F4EA;
--warning: #B24020;                  /* Amber - caution */
--warning-light: #FCE8E6;
--error: #CC1016;                    /* Red - errors */
--error-light: #FCE8E6;
--info: #0A66C2;                     /* LinkedIn blue - info */
```

### Typography

**Font Stack**
```css
--font-primary: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
--font-mono: "SF Mono", "Monaco", "Inconsolata", "Fira Code", monospace;
```

**Type Scale**
```css
--text-xs: 0.75rem;     /* 12px - captions, metadata */
--text-sm: 0.875rem;    /* 14px - small text, timestamps */
--text-base: 1rem;      /* 16px - body text */
--text-md: 1.125rem;    /* 18px - lead text */
--text-lg: 1.25rem;     /* 20px - subheadings */
--text-xl: 1.5rem;      /* 24px - section titles */
--text-2xl: 1.75rem;    /* 28px - page titles */
--text-3xl: 2rem;       /* 32px - large headings */
--text-4xl: 2.5rem;     /* 40px - display */
```

**Font Weights**
```css
--font-regular: 400;
--font-medium: 500;
--font-semibold: 600;
--font-bold: 700;
```

### Spacing System

```css
--space-1: 0.25rem;   /* 4px */
--space-2: 0.5rem;    /* 8px */
--space-3: 0.75rem;   /* 12px */
--space-4: 1rem;      /* 16px */
--space-5: 1.25rem;   /* 20px */
--space-6: 1.5rem;    /* 24px */
--space-8: 2rem;      /* 32px */
--space-10: 2.5rem;   /* 40px */
--space-12: 3rem;     /* 48px */
--space-16: 4rem;     /* 64px */
```

### UI Component Styling

**Cards**
```css
.card-linkedin {
  background: var(--bg-card);
  border-radius: 8px;
  box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.15), 0 2px 3px rgba(0, 0, 0, 0.1);
  border: none;
  transition: box-shadow 0.2s ease;
}

.card-linkedin:hover {
  box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.15), 0 4px 6px rgba(0, 0, 0, 0.1);
}
```

**Buttons**
```css
/* Primary - LinkedIn Blue */
.btn-primary {
  background: var(--linkedin-blue);
  color: var(--text-light);
  font-weight: 600;
  padding: 10px 24px;
  border-radius: 24px;
  border: none;
  transition: background-color 0.2s ease;
}

.btn-primary:hover {
  background: var(--linkedin-blue-dark);
}

/* Secondary - Outline */
.btn-secondary {
  background: transparent;
  border: 1.5px solid var(--linkedin-blue);
  color: var(--linkedin-blue);
  padding: 10px 24px;
  border-radius: 24px;
  font-weight: 600;
  transition: all 0.2s ease;
}

.btn-secondary:hover {
  background: var(--linkedin-blue-light);
  border-color: var(--linkedin-blue-dark);
}

/* Tertiary - Ghost */
.btn-tertiary {
  background: transparent;
  color: var(--text-secondary);
  padding: 8px 16px;
  border-radius: 4px;
  font-weight: 600;
  transition: background-color 0.2s ease;
}

.btn-tertiary:hover {
  background: var(--bg-hover);
  color: var(--text-primary);
}
```

**Form Inputs**
```css
.input-linkedin {
  background: var(--bg-secondary);
  border: 1px solid var(--color-gray-300);
  border-radius: 4px;
  padding: 12px 16px;
  font-size: var(--text-base);
  transition: border-color 0.2s ease, box-shadow 0.2s ease;
}

.input-linkedin:focus {
  border-color: var(--linkedin-blue);
  box-shadow: 0 0 0 1px var(--linkedin-blue);
  outline: none;
}
```

**Avatar Styles**
```css
.avatar-sm {
  width: 32px;
  height: 32px;
  border-radius: 50%;
}

.avatar-md {
  width: 48px;
  height: 48px;
  border-radius: 50%;
}

.avatar-lg {
  width: 72px;
  height: 72px;
  border-radius: 50%;
}

.avatar-xl {
  width: 128px;
  height: 128px;
  border-radius: 50%;
}
```

### Layout Principles

**Grid System**
- Use 12-column grid for flexibility
- Maximum content width: 1128px (LinkedIn's standard max-width)
- Sidebar width: 225px (left), 300px (right on desktop)
- Main feed: flexible center column
- Consistent gutters: 24px (desktop), 16px (mobile)

**Section Spacing**
```css
.section {
  padding: var(--space-6) 0; /* 24px vertical */
}

.section-lg {
  padding: var(--space-8) 0;  /* 32px vertical */
}

.card-padding {
  padding: var(--space-4) var(--space-4); /* 16px all sides */
}
```

**Visual Hierarchy**
- Clear distinction between primary and secondary content
- Use LinkedIn blue sparingly for primary actions and links
- Generous whitespace for readability
- Content-first approach with minimal chrome

### Animation & Transitions

```css
/* Quick, subtle animations */
--transition-fast: 167ms ease;
--transition-base: 200ms ease;
--transition-slow: 300ms ease;

/* Focus states */
--focus-ring: 0 0 0 1px var(--linkedin-blue), 0 0 0 4px var(--linkedin-blue-light);

/* Entrance animations */
@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

/* Subtle scale on interaction */
.interactive:active {
  transform: scale(0.98);
}
```

### Design Principles for Professional Networking

1. **Professionalism**
   - Clean, business-focused layouts
   - Conservative color palette with strategic use of LinkedIn blue
   - Readable typography hierarchy
   - Subtle, functional micro-interactions

2. **Trust & Authenticity**
   - Clear user identity representation
   - Transparent information hierarchy
   - Consistent UI patterns
   - Professional imagery standards

3. **Connection & Engagement**
   - Clear call-to-action buttons
   - Easy-to-scan content cards
   - Prominent profile and network features
   - Accessible interaction patterns

4. **Efficiency**
   - Fast load times and smooth transitions
   - Intuitive navigation patterns
   - Scannable content layouts
   - Keyboard-accessible interactions

---

## System Architecture Principles

### Separation of Concerns
- Keep UI, business logic, and data access layers separate
- Each module/component should have a single, well-defined responsibility
- Avoid mixing concerns within the same file or function

### Modularity
- Design components to be self-contained and reusable
- Use clear interfaces between modules
- Minimize dependencies between unrelated modules

### Scalability
- Design systems to handle increased load gracefully
- Use stateless components where possible
- Consider horizontal scaling in architecture decisions

---

## Design Patterns

### Component Architecture (Next.js/React)
```
app/
├── components/           # Reusable UI components
│   ├── ui/              # Base UI elements (Button, Input, Card)
│   ├── layout/          # Layout components (Header, Footer, Sidebar)
│   └── features/        # Feature-specific components
├── hooks/               # Custom React hooks
├── lib/                 # Utility functions and helpers
├── services/            # API and external service integrations
├── types/               # TypeScript type definitions
└── constants/           # Application constants
```

### Server vs Client Components
- **Default to Server Components** for better performance
- Use Client Components (`'use client'`) only when:
  - Using React hooks (useState, useEffect, etc.)
  - Handling user interactions (onClick, onChange)
  - Accessing browser-only APIs
  - Using third-party client libraries

### Data Flow Patterns
- **Unidirectional data flow**: Props down, events up
- Use React Context sparingly for truly global state
- Prefer composition over prop drilling
- Colocate state as close to where it's used as possible

### API Design
- Follow RESTful conventions for API routes
- Use consistent response structures:
  ```typescript
  interface ApiResponse<T> {
    success: boolean;
    data?: T;
    error?: {
      code: string;
      message: string;
    };
  }
  ```
- Implement proper error handling and status codes
- Version APIs when breaking changes are necessary

---

## Security Protocols

### Authentication & Authorization
- Never expose sensitive credentials in client-side code
- Use environment variables for secrets (`.env.local`)
- Implement proper session management
- Validate user permissions on both client and server

### Data Protection
- Sanitize all user inputs
- Use parameterized queries to prevent SQL injection
- Implement CSRF protection for forms
- Validate and sanitize data on the server, never trust client input

### API Security
- Implement rate limiting on API routes
- Use HTTPS for all communications
- Validate request origins with CORS policies
- Never expose internal error details to clients

### Environment Variables
```bash
# Public (exposed to browser) - prefix with NEXT_PUBLIC_
NEXT_PUBLIC_API_URL=https://api.example.com

# Private (server-only) - no prefix
DATABASE_URL=postgresql://...
API_SECRET_KEY=...
```

---

## Code Organization Standards

### File Naming
| Type | Convention | Example |
|------|------------|---------|
| Components | PascalCase | `UserProfile.tsx` |
| Hooks | camelCase with `use` prefix | `useAuth.ts` |
| Utilities | camelCase | `formatDate.ts` |
| Types/Interfaces | PascalCase | `User.types.ts` |
| Constants | UPPER_SNAKE_CASE | `API_ENDPOINTS.ts` |
| Routes/Pages | lowercase-kebab | `user-settings/page.tsx` |

### Import Organization
```typescript
// 1. External libraries
import { useState, useEffect } from 'react';
import Image from 'next/image';

// 2. Internal modules (absolute imports)
import { Button } from '@/components/ui/Button';
import { useAuth } from '@/hooks/useAuth';

// 3. Types
import type { User } from '@/types/User';

// 4. Relative imports (styles, local files)
import styles from './Component.module.css';
```

### Absolute Imports
Configure and use absolute imports for cleaner paths:
```typescript
// ✅ Good
import { Button } from '@/components/ui/Button';

// ❌ Avoid
import { Button } from '../../../components/ui/Button';
```

---

## Error Handling Architecture

### Error Boundaries
- Implement error boundaries for graceful failure handling
- Provide user-friendly error messages
- Log errors for debugging (server-side)

### Try-Catch Patterns
```typescript
async function fetchData(): Promise<Result<Data, Error>> {
  try {
    const response = await fetch('/api/data');
    if (!response.ok) {
      throw new Error(`HTTP ${response.status}`);
    }
    const data = await response.json();
    return { success: true, data };
  } catch (error) {
    console.error('Failed to fetch data:', error);
    return { success: false, error };
  }
}
```

### Error Logging
- Use structured logging format
- Include context (user ID, request ID, timestamp)
- Never log sensitive information (passwords, tokens)

---

## Performance Guidelines

### Rendering Optimization
- Use React.memo() for expensive pure components
- Implement proper key props for lists
- Avoid inline function definitions in JSX
- Use useMemo/useCallback appropriately (not everywhere)

### Data Fetching
- Leverage Next.js caching strategies
- Implement loading and error states
- Use optimistic updates for better UX
- Deduplicate requests where possible

### Bundle Optimization
- Use dynamic imports for code splitting
- Analyze bundle size regularly
- Tree-shake unused code
- Lazy load below-the-fold content

---

## Testing Architecture

### Test Structure
```
__tests__/
├── unit/           # Unit tests for functions/hooks
├── components/     # Component tests
├── integration/    # Integration tests
└── e2e/           # End-to-end tests
```

### Testing Priorities
1. **Critical paths**: Authentication, payments, core features
2. **Business logic**: Utility functions, calculations
3. **Component behavior**: User interactions
4. **Edge cases**: Error states, empty states

---

## Documentation Requirements

### Code Documentation
- Document complex business logic with comments
- Use JSDoc for public APIs and utilities
- Keep README files updated
- Document architectural decisions (ADRs)

### Component Documentation
```typescript
/**
 * Button component with LinkedIn design styling.
 * 
 * @param label - Button text content
 * @param variant - Visual style variant (primary, secondary, tertiary)
 * @param onClick - Click handler function
 * @param disabled - Whether the button is disabled
 * @param size - Button size (sm, md, lg)
 * 
 * @example
 * <Button label="Connect" variant="primary" onClick={handleConnect} />
 */
```

---

## Compliance Checklist

Before merging code, ensure:
- [ ] Follows separation of concerns
- [ ] Uses appropriate design patterns
- [ ] Implements proper error handling
- [ ] Follows security protocols
- [ ] Has necessary documentation
- [ ] Passes all tests
- [ ] No sensitive data exposed
- [ ] Follows naming conventions
