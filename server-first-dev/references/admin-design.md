# Administration And Workbench UI Design

**Scope:** application `/admin`, server workbench, secrets UI, monitoring, readiness/to-dos, backup visibility—not public marketing pages (use [frontend-design.md](frontend-design.md)).

Embedded from the local `administration-design` skill for `server-first-dev`. Navigation and labels must match the **actual product**, not generic placeholders.

## Style Identity

- shadcn v4, `radix-nova`, neutral base, Tailwind v4 CSS-first (`src/index.css` theme source)
- Geist UI font
- Light mode default (no theme switcher unless requested)
- Warm yellow/gold primary, neutral surfaces, compact controls, high-radius surfaces, soft Luma shadows
- Hugeicons for shadcn primitives when configured; `lucide-react` for nav and feature icons

## App Shell

Authenticated admin/workbench pages:

```tsx
<SidebarProvider>
  <div className="app-shell flex h-svh w-full overflow-hidden bg-surface/40">
    <div className="hidden md:block">
      <AppSidebar />
    </div>
    <div className="flex min-w-0 flex-1 flex-col overflow-hidden">
      <AppMobileHeader />
      <header className="hidden h-14 items-center gap-3 border-b border-border/70 bg-background/85 px-5 backdrop-blur md:flex">
        <SidebarTrigger className="-ml-1" />
        {/* breadcrumbs */}
        <div className="ml-auto flex items-center gap-3 text-xs text-muted-foreground">
          {/* optional status */}
        </div>
      </header>
      <main className="min-h-0 flex-1 overflow-auto bg-transparent">
        <Outlet />
      </main>
    </div>
  </div>
  <AppMobileMenu />
</SidebarProvider>
```

Rules: `h-svh` not `h-screen`; shell `overflow-hidden`, main `overflow-auto`; desktop sidebar hidden below `md`; custom mobile header + Sheet menu; `min-w-0` on flex children.

## Sidebar

- `collapsible="icon"`, fixed desktop sidebar with layout gap so content never underlaps
- Expanded: logo `h-11 w-11` (often `brightness-0`), product name + "Administration" subtitle, group labels uppercase tracked
- Collapsed: icon-only with tooltips
- Footer: account dropdown (avatar, name, email, settings, logout)
- Nav groups by domain: Management, Content, Operations, People, System—only if they fit the product

## Mobile

- Header `h-14` with logo, title, menu trigger
- Sheet menu mirrors desktop sections; close on navigate

## Page Layout

Default:

```tsx
<div className="p-6 space-y-5">
  <div className="flex flex-col gap-3 sm:flex-row sm:items-center sm:justify-between">
    <div>
      <h1 className="text-2xl font-semibold tracking-tight">Page Title</h1>
      <p className="text-sm text-muted-foreground">Short description.</p>
    </div>
    <Button>Primary action</Button>
  </div>
</div>
```

Dense ops pages: `p-3 sm:p-6 space-y-3 sm:space-y-4`.

## Component Rules

- Compact controls: `h-8`, `rounded-lg`, `text-sm`
- Subtle destructive styling (not solid red blocks)
- Tables: standalone `rounded-2xl border ...` shells; clickable rows; stop propagation on row actions
- No one-item kebab menus—direct icon for single actions like delete
- No manual refresh buttons by default—sockets or query invalidation
- No decorative stat cards unless they drive action
- Disable save when form unchanged
- `tabular-nums` for numbers; default locale `cs-CZ`, 24h time unless product specifies otherwise

## Tokens

Expose shadcn tokens plus `sidebar-*`, semantic `success/warning/info/surface/brand`, `shadow-luma-*`, radius scale in `@theme inline`.

## Workbench-Specific

- Read-only posture: status, logs, backups, checklist—no restart/restore buttons by default
- Secrets page follows [secrets.md](secrets.md) UX (last-four display)

## Mistakes To Avoid

- Stock shadcn spacing and generic sidebar mobile mode
- Tailwind config file when v4 CSS-first is enough
- Wrapping every table in a heavy Card
- Exposing internal tech names in user-facing copy
