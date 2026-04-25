---
name: ui components
description: Production-grade frontend UI component best practices.
---

# UI Components

## Instructions

Follow this guide when building frontend UI components.

1. **Responsive by default**
   - Every component must work on mobile and desktop.
   - Use fluid layouts (flex/grid) over fixed pixel widths.
   - Test at 320px, 768px, and 1280px breakpoints.

2. **Accessibility**
   - Use semantic HTML (`button`, `nav`, `header`, `main`).
   - Provide `aria-label` for icon-only controls.
   - Ensure keyboard navigation works (tab order, focus rings, Esc to close).
   - Maintain WCAG AA contrast ratios.

3. **Component structure**
   - One component per file.
   - Co-locate styles, tests, and types with the component.
   - Keep props explicit and typed; avoid spreading unknown props.

4. **State management**
   - Lift state only as far as needed.
   - Prefer derived state over duplicated state.
   - Keep side effects in hooks, not render bodies.

5. **Styling**
   - Use the project's design tokens for color, spacing, and typography.
   - Avoid inline styles except for dynamic values.
   - No magic numbers — reference tokens or named constants.

6. **Performance**
   - Memoize expensive computations.
   - Lazy-load route-level components.
   - Avoid re-rendering large lists; virtualize when over ~100 items.
