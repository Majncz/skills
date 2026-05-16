# Frontend Design (Public / Customer-Facing Pages)

**Scope:** presentation websites, landing pages, marketing sections, customer-facing shop UI—not admin or server workbench (use [admin-design.md](admin-design.md) there).

## Attribution

Adapted from Anthropic's `frontend-design` skill (Apache License 2.0). See [licenses/frontend-design-APACHE-2.0.txt](../licenses/frontend-design-APACHE-2.0.txt). This file is modified for use inside `server-first-dev`.

---

## Design Thinking

Before coding, understand context and commit to a **bold** aesthetic direction:

- **Purpose:** Who uses this and what problem does it solve?
- **Tone:** Pick a clear direction—minimal, maximalist, retro-futuristic, luxury, playful, editorial, brutalist, art deco, industrial, etc.
- **Constraints:** React + Vite, performance, accessibility.
- **Differentiation:** One memorable hook—layout, type, color, or motion.

Intentionality beats intensity. Minimal and maximal both work when executed precisely.

## Implementation

- Production-grade, working code.
- Cohesive visual point of view.
- Refine details; match complexity to the vision.

## Aesthetics Guidelines

### Typography

Distinctive fonts—avoid default AI choices (Inter, Roboto, Arial, system UI). Pair a display face with a refined body font.

### Color And Theme

CSS variables; dominant palette with sharp accents. Avoid clichéd purple-on-white gradients.

### Motion

CSS-first where possible; Motion library in React when needed. Prefer one strong page-load sequence over scattered micro-interactions. Scroll and hover surprises where appropriate.

### Spatial Composition

Asymmetry, overlap, grid-breaking, generous negative space or controlled density.

### Backgrounds

Depth: gradients, noise, patterns, layered transparency, grain—not flat gray boxes.

## Avoid

- Generic "AI slop" layouts and component patterns.
- Same font across every project (e.g. Space Grotesk every time).
- Overused purple gradients on white.

Vary light/dark, fonts, and mood per business context (cafe ≠ law firm ≠ SaaS).

## Complexity

Maximalist designs need more code and animation. Minimal designs need restraint in spacing and type. Execute the chosen direction well.
