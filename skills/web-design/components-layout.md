---
name: components-layout
description: Layout components for page structure - Container, Grid, Section, Stack
---

# Layout Components

Foundational components for page structure and content organization.

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

## Container

**Purpose**: Max-width wrapper that centers content and adds horizontal padding.

**When to use**: Wrap all page content, sections, or constrain wide layouts.

**Usual contents**: Any page content that needs width constraints.

**Structure**:

```tsx
<div className="container mx-auto px-4 md:px-6 lg:px-8">{children}</div>
```

**Variants**:
| Variant | Max Width | Use Case |
|---------|-----------|----------|
| `sm` | 640px | Narrow content (articles, forms) |
| `md` | 768px | Medium content |
| `lg` | 1024px | Standard pages |
| `xl` | 1280px | Wide layouts |
| `2xl` | 1400px | Full-width dashboards |
| `full` | 100% | Edge-to-edge (with padding) |

**Responsive padding**:

```tsx
// Tighter on mobile, roomier on desktop
className = "px-4 sm:px-6 lg:px-8";
```

**Accessibility**: None specific - semantic wrapper only.

**Refs**:

- Tailwind Container: https://tailwindcss.com/docs/container

---

## Section

**Purpose**: Vertical page section with consistent spacing.

**When to use**: Separate distinct content areas (hero, features, testimonials, etc.).

**Usual contents**: Section header (optional), content, CTA (optional).

**Structure**:

```tsx
<section className="py-16 md:py-24 lg:py-32">
  <div className="container">
    {/* Optional section header */}
    <div className="mx-auto max-w-2xl text-center mb-12">
      <h2 className="text-3xl font-bold tracking-tight sm:text-4xl">Section Title</h2>
      <p className="mt-4 text-lg text-muted-foreground">Section description text</p>
    </div>

    {/* Section content */}
    {children}
  </div>
</section>
```

**Variants**:
| Variant | Padding | Use Case |
|---------|---------|----------|
| `sm` | py-8 md:py-12 | Tight sections |
| `default` | py-16 md:py-24 | Standard sections |
| `lg` | py-24 md:py-32 | Spacious sections |
| `hero` | py-24 md:py-32 lg:py-40 | Hero/above-fold |

**Background variations**:

```tsx
// Alternating backgrounds
<section className="bg-muted/50">
<section className="bg-background">

// Gradient backgrounds
<section className="bg-gradient-to-b from-muted/50 to-background">
```

**Accessibility**: Use `<section>` with `aria-labelledby` pointing to heading.

---

## Grid

**Purpose**: Multi-column responsive layouts.

**When to use**: Card grids, feature lists, gallery layouts.

**Usual contents**: Repeated items (cards, features, images).

**Structure**:

```tsx
{
  /* Responsive grid: 1 col → 2 col → 3 col */
}
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
  {items.map((item) => (
    <Card key={item.id}>{item.content}</Card>
  ))}
</div>;
```

**Common patterns**:

```tsx
// 2-column split
<div className="grid md:grid-cols-2 gap-8 items-center">

// 4-column features
<div className="grid sm:grid-cols-2 lg:grid-cols-4 gap-6">

// Asymmetric (content + sidebar)
<div className="grid lg:grid-cols-[1fr_300px] gap-8">

// Auto-fit (responsive without breakpoints)
<div className="grid grid-cols-[repeat(auto-fit,minmax(280px,1fr))] gap-6">
```

**Gap scale**:
| Gap | Pixels | Use Case |
|-----|--------|----------|
| `gap-4` | 16px | Tight grid |
| `gap-6` | 24px | Default |
| `gap-8` | 32px | Spacious |
| `gap-12` | 48px | Very spacious |

**Accessibility**: Use semantic lists (`<ul>`) for card grids when appropriate.

**Refs**:

- Tailwind Grid: https://tailwindcss.com/docs/grid-template-columns

---

## Stack

**Purpose**: Vertical or horizontal spacing between elements.

**When to use**: Consistent spacing between child elements.

**Usual contents**: Any vertically or horizontally stacked items.

**Structure**:

```tsx
{
  /* Vertical stack */
}
<div className="flex flex-col gap-4">
  <Item />
  <Item />
  <Item />
</div>;

{
  /* Horizontal stack */
}
<div className="flex flex-row gap-4 items-center">
  <Item />
  <Item />
</div>;

{
  /* Horizontal with wrap */
}
<div className="flex flex-wrap gap-4">
  <Tag />
  <Tag />
  <Tag />
</div>;
```

**Variants**:
| Direction | Classes |
|-----------|---------|
| Vertical | `flex flex-col` |
| Horizontal | `flex flex-row` |
| Responsive | `flex flex-col md:flex-row` |

**Alignment**:

```tsx
// Vertical alignment (for horizontal stacks)
items - start; // Top
items - center; // Center
items - end; // Bottom
items - baseline; // Text baseline

// Horizontal alignment (for vertical stacks)
justify - start; // Left
justify - center; // Center
justify - end; // Right
justify - between; // Space between
```

**Accessibility**: None specific - layout only.

---

## Sidebar Layout

**Purpose**: App shell with fixed/collapsible sidebar and main content area.

**When to use**: Dashboards, admin panels, settings pages.

**Usual contents**: Navigation sidebar + main content area.

**Structure**:

```tsx
<div className="flex min-h-screen">
  {/* Sidebar */}
  <aside className="hidden md:flex w-64 flex-col border-r bg-muted/40">
    <div className="flex h-14 items-center border-b px-4">
      <Logo />
    </div>
    <nav className="flex-1 space-y-1 p-4">
      <NavItems />
    </nav>
    <div className="border-t p-4">
      <UserMenu />
    </div>
  </aside>

  {/* Main content */}
  <div className="flex flex-1 flex-col">
    <header className="flex h-14 items-center border-b px-4 md:px-6">
      <MobileMenuTrigger className="md:hidden" />
      <HeaderContent />
    </header>
    <main className="flex-1 p-4 md:p-6">{children}</main>
  </div>
</div>
```

**Variants**:
| Variant | Behavior |
|---------|----------|
| Fixed | Sidebar always visible on desktop |
| Collapsible | Can collapse to icons only |
| Overlay | Mobile: slides over content |
| Inset | Content has its own scroll |

**Collapsible sidebar pattern**:

```tsx
const [collapsed, setCollapsed] = useState(false)

<aside className={cn(
  "transition-all duration-300",
  collapsed ? "w-16" : "w-64"
)}>
```

**Mobile drawer**:

```tsx
// Use Sheet component for mobile nav
<Sheet>
  <SheetTrigger asChild>
    <Button variant="ghost" size="icon" className="md:hidden">
      <Menu className="h-5 w-5" />
    </Button>
  </SheetTrigger>
  <SheetContent side="left" className="w-64 p-0">
    <MobileNav />
  </SheetContent>
</Sheet>
```

**Accessibility**:

- Sidebar should be `<aside>` or `<nav>`
- Use `aria-expanded` for collapsible state
- Skip link to main content

**Refs**:

- shadcn Sidebar: https://ui.shadcn.com/docs/components/sidebar
- Radix Sheet: https://www.radix-ui.com/primitives/docs/components/dialog

---

## Aspect Ratio

**Purpose**: Maintain consistent aspect ratios for media containers.

**When to use**: Images, videos, embeds that need fixed proportions.

**Usual contents**: Images, videos, iframes.

**Structure**:

```tsx
<div className="aspect-video overflow-hidden rounded-lg">
  <img src="/image.jpg" alt="Description" className="h-full w-full object-cover" />
</div>
```

**Common ratios**:
| Ratio | Class | Use Case |
|-------|-------|----------|
| 1:1 | `aspect-square` | Avatars, thumbnails |
| 16:9 | `aspect-video` | Videos, hero images |
| 4:3 | `aspect-[4/3]` | Photos |
| 3:2 | `aspect-[3/2]` | Landscape photos |
| 21:9 | `aspect-[21/9]` | Ultra-wide banners |

**With shadcn AspectRatio**:

```tsx
import { AspectRatio } from "@/components/ui/aspect-ratio";

<AspectRatio ratio={16 / 9}>
  <Image src="/image.jpg" alt="Photo" fill className="object-cover" />
</AspectRatio>;
```

**Accessibility**: Always include `alt` text for images.

**Refs**:

- shadcn Aspect Ratio: https://ui.shadcn.com/docs/components/aspect-ratio
- Tailwind Aspect Ratio: https://tailwindcss.com/docs/aspect-ratio

---

## Separator / Divider

**Purpose**: Visual separation between content sections.

**When to use**: Between list items, form sections, sidebar groups.

**Usual contents**: None (decorative element).

**Structure**:

```tsx
{/* Horizontal separator */}
<hr className="border-t border-border" />

{/* With shadcn */}
import { Separator } from "@/components/ui/separator"

<Separator />
<Separator orientation="vertical" className="h-6" />
```

**Variants**:

```tsx
// Horizontal (default)
<Separator />

// Vertical (must set height)
<Separator orientation="vertical" className="h-4" />

// With text
<div className="relative">
  <Separator />
  <span className="absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2 bg-background px-2 text-xs text-muted-foreground">
    OR
  </span>
</div>

// Decorative (muted)
<Separator className="bg-muted" />
```

**Spacing patterns**:

```tsx
// In a list
<div className="space-y-4 divide-y">

// Explicit spacing
<Separator className="my-6" />
```

**Accessibility**:

- Use `<hr>` for semantic separation
- `role="separator"` added by shadcn component
- `aria-orientation` for vertical separators

**Refs**:

- shadcn Separator: https://ui.shadcn.com/docs/components/separator

---

## Layout Composition Example

Putting it all together:

```tsx
export default function FeaturePage() {
  return (
    <div className="flex min-h-screen">
      {/* Sidebar */}
      <Sidebar />

      {/* Main content */}
      <div className="flex flex-1 flex-col">
        <Header />

        <main className="flex-1">
          {/* Hero section */}
          <Section variant="hero">
            <Container size="lg">
              <HeroContent />
            </Container>
          </Section>

          {/* Features grid */}
          <Section className="bg-muted/50">
            <Container>
              <SectionHeader title="Features" description="Everything you need" />
              <Grid cols={3} gap={6}>
                {features.map((f) => (
                  <FeatureCard key={f.id} {...f} />
                ))}
              </Grid>
            </Container>
          </Section>

          {/* CTA section */}
          <Section>
            <Container size="md" className="text-center">
              <CTAContent />
            </Container>
          </Section>
        </main>

        <Footer />
      </div>
    </div>
  );
}
```

## Split Layout

**Purpose**: Two-column layout with content and sidebar.

**When to use**: Documentation pages, blog posts with TOC, product pages with filters.

**Structure**:

```tsx
<div className="grid lg:grid-cols-[1fr_280px] gap-8">
  {/* Main content */}
  <article className="min-w-0">
    <h1>{title}</h1>
    <div className="prose">{content}</div>
  </article>

  {/* Sidebar */}
  <aside className="hidden lg:block">
    <div className="sticky top-20 space-y-6">
      <TableOfContents />
      <RelatedLinks />
    </div>
  </aside>
</div>
```

**Variants**:
| Variant | Ratio | Use Case |
|---------|-------|----------|
| `70/30` | `[1fr_300px]` | Content heavy |
| `60/40` | `[3fr_2fr]` | Balanced |
| `50/50` | `grid-cols-2` | Equal split |

**Responsive behavior**:

```tsx
// Sidebar below content on mobile
<div className="grid grid-cols-1 lg:grid-cols-[1fr_300px] gap-8">

// Sidebar collapses to drawer on mobile
<aside className="hidden lg:block">
```

**Accessibility**: Use `<article>` for main content, `<aside>` for sidebar.

---

## Sticky Header

**Purpose**: Fixed header that stays visible while scrolling.

**When to use**: Navigation, dashboards, long-scrolling pages.

**Structure**:

```tsx
<div className="min-h-screen">
  {/* Sticky header */}
  <header className="sticky top-0 z-50 border-b bg-background/95 backdrop-blur supports-[backdrop-filter]:bg-background/60">
    <div className="container flex h-14 items-center">
      <Logo />
      <nav className="ml-auto flex gap-4">
        <NavLinks />
      </nav>
    </div>
  </header>

  {/* Scrollable content */}
  <main className="container py-8">{content}</main>
</div>
```

**Variants**:

```tsx
// With blur effect
<header className="sticky top-0 z-50 bg-background/80 backdrop-blur-md">

// With shadow on scroll (requires JS)
<header className={cn(
  "sticky top-0 z-50 transition-shadow",
  scrolled && "shadow-sm"
)}>

// Double header (breadcrumbs below)
<header className="sticky top-0 z-50">
  <div className="border-b py-4">Main nav</div>
  <div className="border-b py-2">Breadcrumbs</div>
</header>
```

**Scroll detection hook**:

```tsx
function useScrolled(threshold = 10) {
  const [scrolled, setScrolled] = useState(false);

  useEffect(() => {
    const handleScroll = () => {
      setScrolled(window.scrollY > threshold);
    };
    window.addEventListener("scroll", handleScroll);
    return () => window.removeEventListener("scroll", handleScroll);
  }, [threshold]);

  return scrolled;
}
```

**Accessibility**:

- Use `z-50` to ensure header stays above content
- Maintain focus order - header first in DOM
- Consider `position: fixed` alternative for true fixed behavior

---

## Masonry Grid

**Purpose**: Pinterest-style grid with items of varying heights.

**When to use**: Image galleries, card layouts with variable content.

**Structure**:

```tsx
// CSS Grid with auto-flow
<div className="columns-1 sm:columns-2 lg:columns-3 gap-4 space-y-4">
  {items.map((item) => (
    <div key={item.id} className="break-inside-avoid">
      <Card>{item.content}</Card>
    </div>
  ))}
</div>
```

**Variants**:
| Columns | Class | Breakpoint |
|---------|-------|------------|
| 1 | `columns-1` | Mobile |
| 2 | `sm:columns-2` | Tablet |
| 3 | `lg:columns-3` | Desktop |
| 4 | `xl:columns-4` | Wide |

**With equal-width items**:

```tsx
// Masonry with consistent widths
<div className="grid grid-cols-[repeat(auto-fill,minmax(250px,1fr))] auto-rows-[10px]">
  {items.map((item, i) => (
    <div
      key={i}
      className="row-span-[var(--rows)]"
      style={{ "--rows": Math.ceil(item.height / 10) }}
    >
      <Card>{item.content}</Card>
    </div>
  ))}
</div>
```

**Accessibility**: Ensure reading order makes sense (top-to-bottom, left-to-right).

---

## Holy Grail Layout

**Purpose**: Classic web layout with header, footer, and three columns.

**When to use**: Admin dashboards, complex applications.

**Structure**:

```tsx
<div className="min-h-screen flex flex-col">
  {/* Header */}
  <header className="border-b">
    <div className="container h-14 flex items-center">
      <Logo />
      <MainNav />
    </div>
  </header>

  {/* Main area */}
  <div className="flex-1 flex">
    {/* Left sidebar */}
    <aside className="w-64 border-r hidden md:block">
      <SecondaryNav />
    </aside>

    {/* Content */}
    <main className="flex-1 container py-6">{children}</main>

    {/* Right sidebar */}
    <aside className="w-64 border-l hidden lg:block">
      <ContextPanel />
    </aside>
  </div>

  {/* Footer */}
  <footer className="border-t py-6">
    <div className="container">
      <FooterContent />
    </div>
  </footer>
</div>
```

**Responsive breakpoints**:

- Mobile: Single column, sidebars in drawers
- Tablet: Left sidebar visible
- Desktop: Both sidebars visible

**Accessibility**:

- Use `<main>` for primary content
- Sidebars as `<aside>` with aria-label
- Skip-to-content link before header

---

## Full-Bleed Layout

**Purpose**: Content that breaks out of container bounds.

**When to use**: Hero images, full-width sections, breakout quotes.

**Structure**:

```tsx
<article className="container max-w-2xl mx-auto px-4">
  {/* Normal content */}
  <p>Article text...</p>

  {/* Full-bleed breakout */}
  <div className="relative left-1/2 right-1/2 -mx-[50vw] w-screen">
    <img src="/hero.jpg" alt="Full width image" className="w-full h-[400px] object-cover" />
  </div>

  {/* Back to normal flow */}
  <p>More article text...</p>
</article>
```

**Alternative with CSS Grid**:

```tsx
<div className="grid grid-cols-[1fr_min(65ch,calc(100%-2rem))_1fr] gap-x-4">
  <div className="col-start-2">
    <p>Normal content</p>
  </div>

  <div className="col-start-1 col-end-4">
    <img src="/full-width.jpg" />
  </div>

  <div className="col-start-2">
    <p>Back to normal</p>
  </div>
</div>
```

**Accessibility**: Ensure full-bleed images have proper alt text and don't disrupt reading flow.

---

## Off-Canvas Layout

**Purpose**: Hidden sidebar that slides in from the edge.

**When to use**: Mobile navigation, shopping cart, filters panel.

**Structure**:

```tsx
<div className="relative overflow-hidden">
  {/* Main content */}
  <div className={cn("transition-transform duration-300", isOpen && "translate-x-[280px]")}>
    <Button onClick={() => setIsOpen(true)}>Open Menu</Button>
    <main>{content}</main>
  </div>

  {/* Off-canvas sidebar */}
  <aside
    className={cn(
      "fixed top-0 left-0 h-full w-[280px] bg-background border-r",
      "transform transition-transform duration-300",
      isOpen ? "translate-x-0" : "-translate-x-full"
    )}
  >
    <Button onClick={() => setIsOpen(false)}>Close</Button>
    <SidebarContent />
  </aside>

  {/* Backdrop */}
  {isOpen && <div className="fixed inset-0 bg-black/50 z-40" onClick={() => setIsOpen(false)} />}
</div>
```

**Variants**:
| Position | Transform | Use Case |
|----------|-----------|----------|
| Left | `-translate-x-full` | Navigation |
| Right | `translate-x-full` | Cart, details |
| Bottom | `translate-y-full` | Mobile sheets |

**Accessibility**:

- Trap focus when open
- Close on Escape key
- aria-hidden on main content when open
- Use Sheet component from shadcn for built-in accessibility

**Refs**:

- shadcn Sheet: https://ui.shadcn.com/docs/components/sheet
