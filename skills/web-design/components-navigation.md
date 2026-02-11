---
name: components-navigation
description: Navigation components - Navbar, Sidebar, Tabs, Breadcrumbs, Footer
---

# Navigation Components

Components for site/app navigation and wayfinding.

---

## Section Schema

Use this template for every component section to keep retrieval reliable:

- **Purpose**
- **When to use**
- **When not to use**
- **Usual contents**
- **Structure**
- **Variants**
- **Accessibility**
- **Refs**

If a field does not apply, write `N/A` instead of omitting it.

---

## Navbar

**Purpose**: Primary site navigation, typically fixed at top.

**When to use**: Every public-facing page, marketing sites, landing pages.

**Usual contents**: Logo, nav links, CTA button, mobile menu trigger.

**Structure**:

```tsx
<header className="sticky top-0 z-50 w-full border-b bg-background/95 backdrop-blur supports-[backdrop-filter]:bg-background/60">
  <div className="container flex h-14 items-center">
    {/* Logo */}
    <Link href="/" className="mr-6 flex items-center space-x-2">
      <Logo className="h-6 w-6" />
      <span className="font-bold">Brand</span>
    </Link>

    {/* Desktop nav */}
    <nav className="hidden md:flex items-center space-x-6 text-sm font-medium">
      <Link href="/features">Features</Link>
      <Link href="/pricing">Pricing</Link>
      <Link href="/about">About</Link>
    </nav>

    {/* Spacer */}
    <div className="flex-1" />

    {/* Actions */}
    <div className="flex items-center space-x-4">
      <Button variant="ghost" size="sm">
        Sign in
      </Button>
      <Button size="sm">Get Started</Button>
    </div>

    {/* Mobile menu trigger */}
    <MobileNav className="md:hidden" />
  </div>
</header>
```

**Variants**:
| Variant | Characteristics |
|---------|-----------------|
| Solid | Opaque background, visible border |
| Transparent | No background until scroll |
| Blur | Semi-transparent with backdrop blur |
| Centered | Logo center, nav items split |

**Scroll behavior**:

```tsx
// Hide on scroll down, show on scroll up
const [hidden, setHidden] = useState(false)
// Use scroll direction hook

// Background on scroll
const [scrolled, setScrolled] = useState(false)
<header className={cn(scrolled && "bg-background/95 border-b")}>
```

**Accessibility**:

- Use `<header>` with `<nav>` inside
- `aria-label="Main navigation"`
- Skip link to main content
- Keyboard navigable

**Refs**:

- shadcn Navigation Menu: https://ui.shadcn.com/docs/components/navigation-menu

---

## Mobile Nav

**Purpose**: Navigation for mobile devices, typically a slide-out drawer.

**When to use**: Responsive counterpart to desktop navbar.

**Usual contents**: Logo, close button, nav links (larger touch targets), CTA.

**Structure**:

```tsx
import { Sheet, SheetContent, SheetTrigger } from "@/components/ui/sheet";

<Sheet>
  <SheetTrigger asChild>
    <Button variant="ghost" size="icon" className="md:hidden">
      <Menu className="h-5 w-5" />
      <span className="sr-only">Toggle menu</span>
    </Button>
  </SheetTrigger>
  <SheetContent side="left" className="w-[300px] sm:w-[400px]">
    <nav className="flex flex-col space-y-4">
      <Link href="/" className="flex items-center space-x-2">
        <Logo className="h-6 w-6" />
        <span className="font-bold">Brand</span>
      </Link>
      <Separator />
      <Link href="/features" className="text-lg font-medium">
        Features
      </Link>
      <Link href="/pricing" className="text-lg font-medium">
        Pricing
      </Link>
      <Link href="/about" className="text-lg font-medium">
        About
      </Link>
      <Separator />
      <Button className="w-full">Get Started</Button>
    </nav>
  </SheetContent>
</Sheet>;
```

**Variants**:
| Variant | Behavior |
|---------|----------|
| Drawer left | Slides from left edge |
| Drawer right | Slides from right edge |
| Full screen | Covers entire viewport |
| Bottom sheet | Slides up from bottom |

**Accessibility**:

- Focus trap when open
- Close on Escape
- Return focus to trigger on close
- `aria-expanded` on trigger

**Refs**:

- shadcn Sheet: https://ui.shadcn.com/docs/components/sheet

---

## Sidebar

**Purpose**: Vertical navigation for apps, dashboards, settings.

**When to use**: Applications with multiple sections/pages.

**Usual contents**: Logo, nav groups with items, user menu, collapse toggle.

**Structure**:

```tsx
<aside className="flex h-screen w-64 flex-col border-r bg-muted/40">
  {/* Header */}
  <div className="flex h-14 items-center border-b px-4">
    <Link href="/" className="flex items-center gap-2 font-semibold">
      <Logo className="h-6 w-6" />
      <span>App Name</span>
    </Link>
  </div>

  {/* Navigation */}
  <nav className="flex-1 space-y-1 overflow-y-auto p-4">
    <NavGroup title="Main">
      <NavItem href="/dashboard" icon={Home}>
        Dashboard
      </NavItem>
      <NavItem href="/projects" icon={Folder}>
        Projects
      </NavItem>
      <NavItem href="/tasks" icon={CheckSquare}>
        Tasks
      </NavItem>
    </NavGroup>
    <NavGroup title="Settings">
      <NavItem href="/settings" icon={Settings}>
        Settings
      </NavItem>
      <NavItem href="/help" icon={HelpCircle}>
        Help
      </NavItem>
    </NavGroup>
  </nav>

  {/* Footer */}
  <div className="border-t p-4">
    <UserMenu />
  </div>
</aside>
```

**Nav Item component**:

```tsx
function NavItem({ href, icon: Icon, children, active }) {
  return (
    <Link
      href={href}
      className={cn(
        "flex items-center gap-3 rounded-lg px-3 py-2 text-sm transition-colors",
        active
          ? "bg-primary text-primary-foreground"
          : "text-muted-foreground hover:bg-muted hover:text-foreground"
      )}
    >
      <Icon className="h-4 w-4" />
      {children}
    </Link>
  );
}
```

**Variants**:
| Variant | Width | Icon | Label |
|---------|-------|------|-------|
| Expanded | 240-280px | Yes | Yes |
| Collapsed | 64-72px | Yes | Tooltip |
| Mini | 48px | Yes | Hidden |

**Accessibility**:

- Use `<nav>` with `aria-label`
- `aria-current="page"` for active item
- Keyboard navigation (arrow keys optional)

**Refs**:

- shadcn Sidebar: https://ui.shadcn.com/docs/components/sidebar

---

## Breadcrumbs

**Purpose**: Show user's location in site hierarchy.

**When to use**: Multi-level pages, nested content, e-commerce categories.

**Usual contents**: Home link, parent pages, current page (not linked).

**Structure**:

```tsx
import {
  Breadcrumb,
  BreadcrumbItem,
  BreadcrumbLink,
  BreadcrumbList,
  BreadcrumbPage,
  BreadcrumbSeparator,
} from "@/components/ui/breadcrumb";

<Breadcrumb>
  <BreadcrumbList>
    <BreadcrumbItem>
      <BreadcrumbLink href="/">Home</BreadcrumbLink>
    </BreadcrumbItem>
    <BreadcrumbSeparator />
    <BreadcrumbItem>
      <BreadcrumbLink href="/products">Products</BreadcrumbLink>
    </BreadcrumbItem>
    <BreadcrumbSeparator />
    <BreadcrumbItem>
      <BreadcrumbPage>Current Product</BreadcrumbPage>
    </BreadcrumbItem>
  </BreadcrumbList>
</Breadcrumb>;
```

**Variants**:

```tsx
// With icons
<BreadcrumbLink href="/"><Home className="h-4 w-4" /></BreadcrumbLink>

// With dropdown for overflow
<BreadcrumbItem>
  <DropdownMenu>
    <DropdownMenuTrigger>
      <MoreHorizontal className="h-4 w-4" />
    </DropdownMenuTrigger>
    <DropdownMenuContent>
      {/* Hidden items */}
    </DropdownMenuContent>
  </DropdownMenu>
</BreadcrumbItem>

// Custom separator
<BreadcrumbSeparator>
  <ChevronRight className="h-4 w-4" />
</BreadcrumbSeparator>
```

**Accessibility**:

- Use `<nav aria-label="Breadcrumb">`
- Last item is not a link
- `aria-current="page"` on current page

**Refs**:

- shadcn Breadcrumb: https://ui.shadcn.com/docs/components/breadcrumb

---

## Tabs

**Purpose**: Switch between related content panels.

**When to use**: Settings sections, content categories, view modes.

**Usual contents**: Tab triggers (labels), tab panels (content).

**Structure**:

```tsx
import { Tabs, TabsContent, TabsList, TabsTrigger } from "@/components/ui/tabs";

<Tabs defaultValue="account" className="w-full">
  <TabsList>
    <TabsTrigger value="account">Account</TabsTrigger>
    <TabsTrigger value="password">Password</TabsTrigger>
    <TabsTrigger value="notifications">Notifications</TabsTrigger>
  </TabsList>
  <TabsContent value="account">
    <AccountForm />
  </TabsContent>
  <TabsContent value="password">
    <PasswordForm />
  </TabsContent>
  <TabsContent value="notifications">
    <NotificationSettings />
  </TabsContent>
</Tabs>;
```

**Variants**:
| Variant | Appearance |
|---------|------------|
| Default | Contained tabs with background |
| Underline | Border-bottom indicator |
| Pills | Rounded pill buttons |
| Vertical | Stacked vertically |

**Underline variant**:

```tsx
<TabsList className="h-auto p-0 bg-transparent border-b rounded-none">
  <TabsTrigger
    value="tab1"
    className="rounded-none border-b-2 border-transparent data-[state=active]:border-primary"
  >
    Tab 1
  </TabsTrigger>
</TabsList>
```

**Accessibility**:

- Automatic: arrow key navigation
- `role="tablist"`, `role="tab"`, `role="tabpanel"`
- `aria-selected` managed by Radix

**Refs**:

- shadcn Tabs: https://ui.shadcn.com/docs/components/tabs
- Radix Tabs: https://www.radix-ui.com/primitives/docs/components/tabs

---

## Pagination

**Purpose**: Navigate through paginated content.

**When to use**: Lists, tables, search results with multiple pages.

**Usual contents**: Previous/next buttons, page numbers, optional page size selector.

**Structure**:

```tsx
import {
  Pagination,
  PaginationContent,
  PaginationItem,
  PaginationLink,
  PaginationNext,
  PaginationPrevious,
  PaginationEllipsis,
} from "@/components/ui/pagination";

<Pagination>
  <PaginationContent>
    <PaginationItem>
      <PaginationPrevious href="#" />
    </PaginationItem>
    <PaginationItem>
      <PaginationLink href="#">1</PaginationLink>
    </PaginationItem>
    <PaginationItem>
      <PaginationLink href="#" isActive>
        2
      </PaginationLink>
    </PaginationItem>
    <PaginationItem>
      <PaginationLink href="#">3</PaginationLink>
    </PaginationItem>
    <PaginationItem>
      <PaginationEllipsis />
    </PaginationItem>
    <PaginationItem>
      <PaginationNext href="#" />
    </PaginationItem>
  </PaginationContent>
</Pagination>;
```

**Variants**:
| Variant | Shows |
|---------|-------|
| Simple | Previous / Next only |
| Numbered | Page numbers |
| Compact | Current / Total only |
| With size | + Page size selector |

**Accessibility**:

- Use `<nav aria-label="Pagination">`
- `aria-current="page"` on active page
- Disabled states for first/last page

**Refs**:

- shadcn Pagination: https://ui.shadcn.com/docs/components/pagination

---

## Footer

**Purpose**: Site-wide footer with links, legal, social.

**When to use**: Every page (marketing sites especially).

**Usual contents**: Logo, link groups, social icons, copyright, legal links.

**Structure**:

```tsx
<footer className="border-t bg-muted/40">
  <div className="container py-12 md:py-16">
    <div className="grid grid-cols-2 gap-8 md:grid-cols-4 lg:grid-cols-5">
      {/* Brand column */}
      <div className="col-span-2 lg:col-span-1">
        <Link href="/" className="flex items-center space-x-2">
          <Logo className="h-6 w-6" />
          <span className="font-bold">Brand</span>
        </Link>
        <p className="mt-4 text-sm text-muted-foreground">Brief company description or tagline.</p>
      </div>

      {/* Link columns */}
      <div>
        <h3 className="font-semibold">Product</h3>
        <ul className="mt-4 space-y-2 text-sm">
          <li>
            <Link href="/features">Features</Link>
          </li>
          <li>
            <Link href="/pricing">Pricing</Link>
          </li>
          <li>
            <Link href="/changelog">Changelog</Link>
          </li>
        </ul>
      </div>

      <div>
        <h3 className="font-semibold">Company</h3>
        <ul className="mt-4 space-y-2 text-sm">
          <li>
            <Link href="/about">About</Link>
          </li>
          <li>
            <Link href="/blog">Blog</Link>
          </li>
          <li>
            <Link href="/careers">Careers</Link>
          </li>
        </ul>
      </div>

      <div>
        <h3 className="font-semibold">Legal</h3>
        <ul className="mt-4 space-y-2 text-sm">
          <li>
            <Link href="/privacy">Privacy</Link>
          </li>
          <li>
            <Link href="/terms">Terms</Link>
          </li>
        </ul>
      </div>
    </div>

    {/* Bottom bar */}
    <div className="mt-12 flex flex-col items-center justify-between gap-4 border-t pt-8 md:flex-row">
      <p className="text-sm text-muted-foreground">© 2024 Brand. All rights reserved.</p>
      <div className="flex space-x-4">
        <Link href="#" aria-label="Twitter">
          <Twitter className="h-5 w-5" />
        </Link>
        <Link href="#" aria-label="GitHub">
          <Github className="h-5 w-5" />
        </Link>
        <Link href="#" aria-label="LinkedIn">
          <Linkedin className="h-5 w-5" />
        </Link>
      </div>
    </div>
  </div>
</footer>
```

**Variants**:
| Variant | Columns | Content |
|---------|---------|---------|
| Simple | 1 | Logo + copyright + social |
| Standard | 4-5 | Multiple link groups |
| Extended | 5+ | + Newsletter, + app badges |

**Accessibility**:

- Use `<footer>` element
- `aria-label` on social icon links
- Group related links

---

## Dropdown Menu

**Purpose**: Contextual actions menu triggered by click.

**When to use**: User menus, action menus, "more" options.

**Usual contents**: Menu items, separators, sub-menus.

**Structure**:

```tsx
import {
  DropdownMenu,
  DropdownMenuContent,
  DropdownMenuItem,
  DropdownMenuLabel,
  DropdownMenuSeparator,
  DropdownMenuTrigger,
} from "@/components/ui/dropdown-menu";

<DropdownMenu>
  <DropdownMenuTrigger asChild>
    <Button variant="ghost" size="icon">
      <MoreHorizontal className="h-4 w-4" />
    </Button>
  </DropdownMenuTrigger>
  <DropdownMenuContent align="end">
    <DropdownMenuLabel>Actions</DropdownMenuLabel>
    <DropdownMenuSeparator />
    <DropdownMenuItem>
      <Edit className="mr-2 h-4 w-4" />
      Edit
    </DropdownMenuItem>
    <DropdownMenuItem>
      <Copy className="mr-2 h-4 w-4" />
      Duplicate
    </DropdownMenuItem>
    <DropdownMenuSeparator />
    <DropdownMenuItem className="text-destructive">
      <Trash className="mr-2 h-4 w-4" />
      Delete
    </DropdownMenuItem>
  </DropdownMenuContent>
</DropdownMenu>;
```

**Accessibility**:

- Full keyboard support (Radix)
- Focus management
- `aria-expanded` on trigger

**Refs**:

- shadcn Dropdown Menu: https://ui.shadcn.com/docs/components/dropdown-menu

---

## Context Menu

**Purpose**: Right-click contextual actions.

**When to use**: Desktop apps, file managers, editors.

**Usual contents**: Same as dropdown menu.

**Structure**:

```tsx
import {
  ContextMenu,
  ContextMenuContent,
  ContextMenuItem,
  ContextMenuTrigger,
} from "@/components/ui/context-menu";

<ContextMenu>
  <ContextMenuTrigger className="flex h-[150px] w-[300px] items-center justify-center rounded-md border border-dashed">
    Right click here
  </ContextMenuTrigger>
  <ContextMenuContent>
    <ContextMenuItem>Copy</ContextMenuItem>
    <ContextMenuItem>Paste</ContextMenuItem>
    <ContextMenuItem>Delete</ContextMenuItem>
  </ContextMenuContent>
</ContextMenu>;
```

**Refs**:

- shadcn Context Menu: https://ui.shadcn.com/docs/components/context-menu

---

## Command Palette

**Purpose**: Keyboard-driven command search and navigation (Cmd+K).

**When to use**: Power user features, app-wide search, quick actions.

**Usual contents**: Search input, categorized commands, keyboard shortcuts.

**Structure**:

```tsx
import {
  CommandDialog,
  CommandEmpty,
  CommandGroup,
  CommandInput,
  CommandItem,
  CommandList,
  CommandSeparator,
} from "@/components/ui/command"

const [open, setOpen] = useState(false)

// Keyboard shortcut
useEffect(() => {
  const down = (e: KeyboardEvent) => {
    if (e.key === "k" && (e.metaKey || e.ctrlKey)) {
      e.preventDefault()
      setOpen((open) => !open)
    }
  }
  document.addEventListener("keydown", down)
  return () => document.removeEventListener("keydown", down)
}, [])

<CommandDialog open={open} onOpenChange={setOpen}>
  <CommandInput placeholder="Type a command or search..." />
  <CommandList>
    <CommandEmpty>No results found.</CommandEmpty>
    <CommandGroup heading="Suggestions">
      <CommandItem>
        <Calendar className="mr-2 h-4 w-4" />
        Calendar
      </CommandItem>
      <CommandItem>
        <Search className="mr-2 h-4 w-4" />
        Search
      </CommandItem>
    </CommandGroup>
    <CommandSeparator />
    <CommandGroup heading="Settings">
      <CommandItem>
        <User className="mr-2 h-4 w-4" />
        Profile
      </CommandItem>
      <CommandItem>
        <Settings className="mr-2 h-4 w-4" />
        Settings
      </CommandItem>
    </CommandGroup>
  </CommandList>
</CommandDialog>
```

**Accessibility**:

- Full keyboard navigation
- Screen reader announcements
- Focus trap when open

**Refs**:

- shadcn Command: https://ui.shadcn.com/docs/components/command
- cmdk: https://cmdk.paco.me/

## Stepper

**Purpose**: Multi-step process indicator with navigation.

**When to use**: Checkout flows, onboarding, wizards, form steps.

**Structure**:

```tsx
<nav aria-label="Progress">
  <ol className="flex items-center w-full">
    {steps.map((step, index) => (
      <li key={step.id} className="flex items-center">
        {/* Step indicator */}
        <div
          className={cn(
            "flex items-center justify-center w-8 h-8 rounded-full text-sm font-medium",
            step.isComplete && "bg-primary text-primary-foreground",
            step.isCurrent && "bg-primary/20 text-primary border-2 border-primary",
            !step.isComplete && !step.isCurrent && "bg-muted text-muted-foreground"
          )}
        >
          {step.isComplete ? <Check className="w-4 h-4" /> : index + 1}
        </div>

        {/* Step label */}
        <span
          className={cn(
            "ml-2 text-sm font-medium",
            step.isComplete && "text-primary",
            step.isCurrent && "text-foreground",
            !step.isComplete && !step.isCurrent && "text-muted-foreground"
          )}
        >
          {step.label}
        </span>

        {/* Connector line */}
        {index < steps.length - 1 && (
          <div className={cn("w-full h-0.5 mx-4", step.isComplete ? "bg-primary" : "bg-muted")} />
        )}
      </li>
    ))}
  </ol>
</nav>
```

**Variants**:
| Variant | Layout | Use Case |
|---------|--------|----------|
| `horizontal` | Inline row | Top of forms |
| `vertical` | Stacked | Side panel |
| `compact` | Icons only | Mobile |

**Vertical stepper**:

```tsx
<ol className="space-y-0">
  {steps.map((step, index) => (
    <li key={step.id} className="flex gap-4">
      {/* Left column: indicator + connector */}
      <div className="flex flex-col items-center">
        <div className="w-8 h-8 rounded-full bg-primary text-primary-foreground flex items-center justify-center">
          {index + 1}
        </div>
        {index < steps.length - 1 && <div className="w-0.5 flex-1 bg-muted my-2" />}
      </div>

      {/* Right column: content */}
      <div className="flex-1 pb-8">
        <h3 className="font-medium">{step.title}</h3>
        <p className="text-sm text-muted-foreground">{step.description}</p>

        {/* Step content */}
        {step.isCurrent && <div className="mt-4">{step.content}</div>}
      </div>
    </li>
  ))}
</ol>
```

**Accessibility**:

- Use `<nav>` with aria-label
- Mark current step with `aria-current="step"`
- Show completed steps with checkmark icon

**Refs**:

- shadcn Stepper: https://ui.shadcn.com/docs/components/stepper

---

## Navigation Link

**Purpose**: Consistent link styling with active states.

**When to use**: Any navigation, replacing raw `<a>` tags.

**Structure**:

```tsx
import { Link, useLocation } from "react-router-dom";
import { cn } from "@/lib/utils";

interface NavLinkProps {
  to: string;
  children: React.ReactNode;
  className?: string;
}

export function NavLink({ to, children, className }: NavLinkProps) {
  const location = useLocation();
  const isActive = location.pathname === to;

  return (
    <Link
      to={to}
      className={cn(
        "inline-flex items-center justify-center px-4 py-2 text-sm font-medium transition-colors",
        "hover:text-primary focus-visible:outline-none focus-visible:ring-2",
        isActive ? "text-primary" : "text-muted-foreground",
        className
      )}
      aria-current={isActive ? "page" : undefined}
    >
      {children}
    </Link>
  );
}
```

**Variants**:

```tsx
// Underline style
<a className={cn(
  "relative py-2 after:absolute after:bottom-0 after:left-0 after:h-0.5",
  "after:w-full after:origin-left after:scale-x-0 after:bg-primary",
  "after:transition-transform hover:after:scale-x-100",
  isActive && "after:scale-x-100"
)}>

// Pill style
<a className={cn(
  "px-4 py-2 rounded-lg transition-colors",
  isActive
    ? "bg-primary text-primary-foreground"
    : "hover:bg-muted"
)}>

// Subtle (footer, secondary nav)
<a className={cn(
  "text-sm text-muted-foreground hover:text-foreground transition-colors",
  isActive && "text-foreground font-medium"
)}>
```

**External links**:

```tsx
<a href={href} target="_blank" rel="noopener noreferrer" className="inline-flex items-center gap-1">
  {children}
  <ExternalLink className="w-3 h-3" />
</a>
```

**Accessibility**:

- Use `aria-current="page"` for active link
- External links: indicate with icon + `rel="noopener noreferrer"`
- Ensure sufficient color contrast

---

## Floating Action Button (FAB)

**Purpose**: Primary action button that floats above content.

**When to use**: Create actions, main CTA on mobile, speed dial.

**Structure**:

```tsx
<button
  className="fixed bottom-6 right-6 z-50 h-14 w-14 rounded-full bg-primary text-primary-foreground shadow-lg hover:shadow-xl transition-shadow"
  aria-label="Create new item"
>
  <Plus className="h-6 w-6 mx-auto" />
</button>
```

**Variants**:
| Variant | Size | Use Case |
|---------|------|----------|
| `default` | 56px | Primary action |
| `small` | 40px | Secondary |
| `extended` | Auto width | With text label |

**Extended FAB**:

```tsx
<button className="fixed bottom-6 right-6 z-50 flex items-center gap-2 px-4 py-3 rounded-full bg-primary text-primary-foreground shadow-lg">
  <Plus className="h-5 w-5" />
  <span className="font-medium">New Task</span>
</button>
```

**Speed dial (multiple actions)**:

```tsx
<div className="fixed bottom-6 right-6 z-50">
  {/* Action buttons */}
  <div
    className={cn(
      "flex flex-col-reverse gap-2 mb-4 transition-all",
      isOpen ? "opacity-100 translate-y-0" : "opacity-0 translate-y-4 pointer-events-none"
    )}
  >
    <button className="h-10 w-10 rounded-full bg-secondary flex items-center justify-center">
      <FileText className="h-4 w-4" />
    </button>
    <button className="h-10 w-10 rounded-full bg-secondary flex items-center justify-center">
      <Image className="h-4 w-4" />
    </button>
  </div>

  {/* Main FAB */}
  <button
    onClick={() => setIsOpen(!isOpen)}
    className="h-14 w-14 rounded-full bg-primary text-primary-foreground shadow-lg"
  >
    <Plus className={cn("h-6 w-6 mx-auto transition-transform", isOpen && "rotate-45")} />
  </button>
</div>
```

**Accessibility**:

- Always use aria-label (icon-only)
- Ensure sufficient touch target (48px minimum)
- Speed dial: trap focus when open

---

## Skip Link

**Purpose**: Allows keyboard users to skip navigation.

**When to use**: All pages with navigation, accessibility requirement.

**Structure**:

```tsx
<a
  href="#main-content"
  className="fixed top-4 left-4 z-[100] -translate-y-[200%] focus:translate-y-0 bg-primary text-primary-foreground px-4 py-2 rounded-md font-medium transition-transform"
>
  Skip to main content
</a>;

{
  /* Later in page */
}
<main id="main-content" tabIndex={-1}>
  {/* Page content */}
</main>;
```

**How it works**:

- Hidden by default (`-translate-y-[200%]`)
- Appears on focus (keyboard tab)
- Clicking jumps to main content
- Focus moves to main content area

**Accessibility**:

- First focusable element in body
- Visible only on keyboard focus
- Main content must have `tabIndex={-1}` to receive focus

---

## Language Selector

**Purpose**: Switch between available languages.

**When to use**: Multi-language sites, i18n implementations.

**Structure**:

```tsx
<DropdownMenu>
  <DropdownMenuTrigger asChild>
    <Button variant="ghost" size="sm" className="gap-2">
      <Globe className="h-4 w-4" />
      <span>EN</span>
    </Button>
  </DropdownMenuTrigger>
  <DropdownMenuContent align="end">
    <DropdownMenuItem onClick={() => setLocale("en")}>
      <span className={cn("mr-2", current === "en" && "font-bold")}>English</span>
      {current === "en" && <Check className="h-4 w-4 ml-auto" />}
    </DropdownMenuItem>
    <DropdownMenuItem onClick={() => setLocale("es")}>
      <span className={cn("mr-2", current === "es" && "font-bold")}>Español</span>
      {current === "es" && <Check className="h-4 w-4 ml-auto" />}
    </DropdownMenuItem>
  </DropdownMenuContent>
</DropdownMenu>
```

**Accessibility**:

- Indicate current language with checkmark
- Use `lang` attribute on html element
- Provide hreflang for alternate versions
