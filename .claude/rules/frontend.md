---
paths:
  - "src/components/**"
  - "src/app/**/page.tsx"
  - "src/app/**/layout.tsx"
  - "src/hooks/**"
---

# Frontend Development Rules

## Design Inspiration (MANDATORY — check before building)
Before creating or modifying any UI component or page:

1. Check if a design brief exists: read `.claude/skills/design-inspiration/DESIGN_BRIEF.md`
   - If it exists, use it as the style guide for all decisions below
2. If no brief, list reference files: `ls .claude/skills/design-inspiration/references/`
   - If references exist (excluding README.md), read each one and extract color, spacing, and component style patterns
   - Apply those patterns directly — do not ask the user to describe the style
3. If neither exists, proceed with the feature spec's visual guidance or ask the user for a style preference

Apply the design language silently — don't narrate the process, just reflect it in Tailwind classes chosen.

## shadcn/ui First (MANDATORY)
- Before creating ANY UI component, check if shadcn/ui has it: `ls src/components/ui/`
- NEVER create custom implementations of: Button, Input, Select, Checkbox, Switch, Dialog, Modal, Alert, Toast, Table, Tabs, Card, Badge, Dropdown, Popover, Tooltip, Navigation, Sidebar, Breadcrumb
- If a shadcn component is missing, install it: `npx shadcn@latest add <name> --yes`
- Custom components are ONLY for business-specific compositions that internally use shadcn primitives

## Import Pattern
```tsx
import { Button } from "@/components/ui/button"
import { Card, CardHeader, CardTitle, CardContent } from "@/components/ui/card"
```

## Component Standards
- Use Tailwind CSS exclusively (no inline styles, no CSS modules)
- All components must be responsive (mobile 375px, tablet 768px, desktop 1440px)
- Implement loading states, error states, and empty states
- Use semantic HTML and ARIA labels for accessibility
- Keep components small and focused
- Use TypeScript interfaces for all props

## Auth Best Practices (Supabase)
- Use `window.location.href` for post-login redirect (not `router.push`)
- Always verify `data.session` exists before redirecting
- Always reset loading state in all code paths (success, error, finally)
