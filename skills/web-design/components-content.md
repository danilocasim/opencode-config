---
name: components-content
description: Content display components - Hero, Card, Avatar, Badge, Testimonial
---

# Content Components

Components for displaying content, media, and information.

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

## Hero

**Purpose**: Above-the-fold attention grabber, typically first section on landing pages.

**When to use**: Landing pages, product pages, marketing pages.

**Usual contents**: Headline, subheadline, CTA buttons, visual (image/video/illustration).

**Structure**:

```tsx
<section className="py-24 md:py-32 lg:py-40">
  <div className="container">
    <div className="mx-auto max-w-3xl text-center">
      {/* Badge/label (optional) */}
      <Badge variant="secondary" className="mb-4">
        New Feature
      </Badge>

      {/* Headline */}
      <h1 className="text-4xl font-bold tracking-tight sm:text-5xl md:text-6xl">
        Build beautiful websites <span className="text-primary">faster than ever</span>
      </h1>

      {/* Subheadline */}
      <p className="mt-6 text-lg text-muted-foreground md:text-xl">
        The modern toolkit for building stunning web experiences. Ship faster with components that
        just work.
      </p>

      {/* CTAs */}
      <div className="mt-10 flex flex-col gap-4 sm:flex-row sm:justify-center">
        <Button size="lg">Get Started</Button>
        <Button size="lg" variant="outline">
          <Play className="mr-2 h-4 w-4" />
          Watch Demo
        </Button>
      </div>
    </div>

    {/* Visual (optional) */}
    <div className="mt-16">
      <div className="aspect-video overflow-hidden rounded-xl border shadow-2xl">
        <Image src="/hero-image.png" alt="Product screenshot" fill />
      </div>
    </div>
  </div>
</section>
```

**Variants**:
| Variant | Layout | Best For |
|---------|--------|----------|
| Centered | Text center, image below | SaaS, apps |
| Split | Text left, image right | Products, portfolios |
| Full-bleed | Background image/video | Bold statements |
| Minimal | Text only, lots of whitespace | Elegant brands |

**Split layout variant**:

```tsx
<div className="grid lg:grid-cols-2 gap-12 items-center">
  <div>{/* Text content */}</div>
  <div>{/* Visual */}</div>
</div>
```

**Accessibility**:

- Use `<h1>` for main headline
- Meaningful alt text for images
- Visible focus on CTAs

---

## Card

**Purpose**: Contained content block with consistent styling.

**When to use**: Grid layouts, feature lists, content previews.

**Usual contents**: Image (optional), title, description, metadata, actions.

**Structure**:

```tsx
import {
  Card,
  CardContent,
  CardDescription,
  CardFooter,
  CardHeader,
  CardTitle,
} from "@/components/ui/card";

<Card>
  <CardHeader>
    <CardTitle>Card Title</CardTitle>
    <CardDescription>Card description or subtitle</CardDescription>
  </CardHeader>
  <CardContent>
    <p>Main content goes here.</p>
  </CardContent>
  <CardFooter>
    <Button>Action</Button>
  </CardFooter>
</Card>;
```

**Variants**:
| Variant | Appearance |
|---------|------------|
| Default | Border, subtle shadow |
| Elevated | Larger shadow, no border |
| Outlined | Border only, no shadow |
| Ghost | No border, no shadow |
| Interactive | Hover state, clickable |

**Interactive card**:

```tsx
<Card className="transition-all hover:shadow-lg hover:-translate-y-1 cursor-pointer">
  {/* Content */}
</Card>

// Or as a link
<Link href="/item/1">
  <Card className="hover:border-primary transition-colors">
    {/* Content */}
  </Card>
</Link>
```

**With image**:

```tsx
<Card className="overflow-hidden">
  <div className="aspect-video">
    <Image src="/image.jpg" alt="" fill className="object-cover" />
  </div>
  <CardHeader>
    <CardTitle>Title</CardTitle>
  </CardHeader>
</Card>
```

**Accessibility**:

- Use semantic headings in CardTitle
- If clickable, entire card should be focusable

**Refs**:

- shadcn Card: https://ui.shadcn.com/docs/components/card

---

## Feature Card

**Purpose**: Highlight a single feature or benefit.

**When to use**: Feature grids, benefits sections, service listings.

**Usual contents**: Icon, title, description.

**Structure**:

```tsx
<div className="flex flex-col items-start gap-4">
  {/* Icon */}
  <div className="rounded-lg bg-primary/10 p-3">
    <Zap className="h-6 w-6 text-primary" />
  </div>

  {/* Title */}
  <h3 className="text-xl font-semibold">Lightning Fast</h3>

  {/* Description */}
  <p className="text-muted-foreground">
    Optimized for speed. Your pages load instantly, keeping users engaged.
  </p>
</div>
```

**Variants**:
| Variant | Icon Position |
|---------|---------------|
| Icon top | Icon above title (default) |
| Icon left | Icon inline with content |
| Icon large | Prominent icon, centered |
| With link | Arrow link at bottom |

**Icon left variant**:

```tsx
<div className="flex gap-4">
  <div className="shrink-0 rounded-lg bg-primary/10 p-3">
    <Icon className="h-6 w-6 text-primary" />
  </div>
  <div>
    <h3 className="font-semibold">Title</h3>
    <p className="mt-1 text-sm text-muted-foreground">Description</p>
  </div>
</div>
```

**Accessibility**:

- Icons should be decorative (`aria-hidden`)
- Use semantic heading level

---

## Avatar

**Purpose**: Represent a user or entity with an image or initials.

**When to use**: User profiles, comments, team lists, testimonials.

**Usual contents**: Image or initials fallback.

**Structure**:

```tsx
import { Avatar, AvatarFallback, AvatarImage } from "@/components/ui/avatar";

<Avatar>
  <AvatarImage src="/avatar.jpg" alt="@username" />
  <AvatarFallback>JD</AvatarFallback>
</Avatar>;
```

**Variants**:
| Size | Class | Pixels | Use Case |
|------|-------|--------|----------|
| sm | `h-8 w-8` | 32px | Compact lists |
| default | `h-10 w-10` | 40px | Standard |
| lg | `h-12 w-12` | 48px | Profiles |
| xl | `h-16 w-16` | 64px | Hero profiles |

**With status indicator**:

```tsx
<div className="relative">
  <Avatar>
    <AvatarImage src="/avatar.jpg" />
    <AvatarFallback>JD</AvatarFallback>
  </Avatar>
  <span className="absolute bottom-0 right-0 h-3 w-3 rounded-full border-2 border-background bg-green-500" />
</div>
```

**Avatar group**:

```tsx
<div className="flex -space-x-4">
  {users.map((user) => (
    <Avatar key={user.id} className="border-2 border-background">
      <AvatarImage src={user.avatar} />
      <AvatarFallback>{user.initials}</AvatarFallback>
    </Avatar>
  ))}
  <Avatar className="border-2 border-background">
    <AvatarFallback>+5</AvatarFallback>
  </Avatar>
</div>
```

**Accessibility**:

- Always include `alt` text
- Initials should be 1-2 characters

**Refs**:

- shadcn Avatar: https://ui.shadcn.com/docs/components/avatar

---

## Badge

**Purpose**: Small status indicator or label.

**When to use**: Status tags, categories, counts, labels.

**Usual contents**: Short text (1-2 words), optional icon.

**Structure**:

```tsx
import { Badge } from "@/components/ui/badge"

<Badge>Default</Badge>
<Badge variant="secondary">Secondary</Badge>
<Badge variant="outline">Outline</Badge>
<Badge variant="destructive">Destructive</Badge>
```

**Variants**:
| Variant | Use Case |
|---------|----------|
| default | Primary labels, key info |
| secondary | Muted, less important |
| outline | Subtle, bordered |
| destructive | Errors, warnings |

**Custom colors** (extend in Tailwind):

```tsx
<Badge className="bg-green-500/10 text-green-500 hover:bg-green-500/20">
  Active
</Badge>
<Badge className="bg-amber-500/10 text-amber-500">
  Pending
</Badge>
```

**With icon**:

```tsx
<Badge>
  <Circle className="mr-1 h-2 w-2 fill-current" />
  Live
</Badge>
```

**Accessibility**:

- Avoid color as only indicator
- Include text description

**Refs**:

- shadcn Badge: https://ui.shadcn.com/docs/components/badge

---

## Stats

**Purpose**: Display key metrics or numbers prominently.

**When to use**: Dashboards, landing pages, reports.

**Usual contents**: Large number, label, optional trend indicator.

**Structure**:

```tsx
<div className="grid gap-4 md:grid-cols-2 lg:grid-cols-4">
  <Card>
    <CardHeader className="flex flex-row items-center justify-between pb-2">
      <CardTitle className="text-sm font-medium">Total Revenue</CardTitle>
      <DollarSign className="h-4 w-4 text-muted-foreground" />
    </CardHeader>
    <CardContent>
      <div className="text-2xl font-bold">$45,231.89</div>
      <p className="text-xs text-muted-foreground">
        <span className="text-green-500">+20.1%</span> from last month
      </p>
    </CardContent>
  </Card>
</div>
```

**Variants**:
| Variant | Layout |
|---------|--------|
| Card | Inside card with icon |
| Inline | Horizontal, compact |
| Centered | Large number centered |
| With chart | Sparkline included |

**Simple inline**:

```tsx
<div className="flex gap-8">
  <div>
    <p className="text-3xl font-bold">10K+</p>
    <p className="text-sm text-muted-foreground">Users</p>
  </div>
  <div>
    <p className="text-3xl font-bold">99.9%</p>
    <p className="text-sm text-muted-foreground">Uptime</p>
  </div>
</div>
```

**Accessibility**:

- Use semantic numbers, not just styled text
- Trend indicators need text description

---

## Testimonial

**Purpose**: Social proof with customer quotes.

**When to use**: Landing pages, case studies, about pages.

**Usual contents**: Quote, avatar, name, role/company.

**Structure**:

```tsx
<figure className="mx-auto max-w-2xl">
  {/* Quote */}
  <blockquote className="text-xl font-medium leading-relaxed">
    "This product has completely transformed how we work. The team couldn't be happier with the
    results."
  </blockquote>

  {/* Attribution */}
  <figcaption className="mt-6 flex items-center gap-4">
    <Avatar>
      <AvatarImage src="/avatar.jpg" />
      <AvatarFallback>JD</AvatarFallback>
    </Avatar>
    <div>
      <p className="font-semibold">Jane Doe</p>
      <p className="text-sm text-muted-foreground">CEO at Company</p>
    </div>
  </figcaption>
</figure>
```

**Variants**:
| Variant | Style |
|---------|-------|
| Simple | Quote + attribution |
| Card | Inside bordered card |
| Large | Big quote marks, prominent |
| With logo | Company logo included |

**Card variant**:

```tsx
<Card className="p-6">
  <div className="flex gap-1 mb-4">
    {[...Array(5)].map((_, i) => (
      <Star key={i} className="h-4 w-4 fill-primary text-primary" />
    ))}
  </div>
  <blockquote className="text-lg">"Quote here..."</blockquote>
  <div className="mt-4 flex items-center gap-3">
    <Avatar className="h-10 w-10">...</Avatar>
    <div>
      <p className="font-medium">Name</p>
      <p className="text-sm text-muted-foreground">Role</p>
    </div>
  </div>
</Card>
```

**Accessibility**:

- Use `<blockquote>` and `<figcaption>`
- Include `cite` if source available

---

## Timeline

**Purpose**: Display chronological events or steps.

**When to use**: History, changelogs, process steps, activity feeds.

**Usual contents**: Date/time, title, description, optional icon.

**Structure**:

```tsx
<div className="space-y-8">
  {events.map((event, index) => (
    <div key={index} className="relative pl-8">
      {/* Line */}
      {index !== events.length - 1 && (
        <div className="absolute left-[11px] top-6 h-full w-px bg-border" />
      )}

      {/* Dot */}
      <div className="absolute left-0 top-1 h-6 w-6 rounded-full border bg-background flex items-center justify-center">
        <div className="h-2 w-2 rounded-full bg-primary" />
      </div>

      {/* Content */}
      <div>
        <time className="text-sm text-muted-foreground">{event.date}</time>
        <h3 className="mt-1 font-semibold">{event.title}</h3>
        <p className="mt-1 text-muted-foreground">{event.description}</p>
      </div>
    </div>
  ))}
</div>
```

**Variants**:
| Variant | Alignment |
|---------|-----------|
| Left | Content on right of line |
| Alternating | Zig-zag layout |
| Centered | Line in middle |

**Accessibility**:

- Use `<time>` element for dates
- Semantic headings for titles

---

## Carousel

**Purpose**: Sliding content panels, one visible at a time.

**When to use**: Image galleries, testimonials, feature showcases.

**Usual contents**: Slides of images, cards, or content.

**Structure**:

```tsx
import {
  Carousel,
  CarouselContent,
  CarouselItem,
  CarouselNext,
  CarouselPrevious,
} from "@/components/ui/carousel";

<Carousel className="w-full max-w-xs">
  <CarouselContent>
    {items.map((item, index) => (
      <CarouselItem key={index}>
        <Card>
          <CardContent className="flex aspect-square items-center justify-center p-6">
            <span className="text-4xl font-semibold">{index + 1}</span>
          </CardContent>
        </Card>
      </CarouselItem>
    ))}
  </CarouselContent>
  <CarouselPrevious />
  <CarouselNext />
</Carousel>;
```

**Variants**:

```tsx
// Multiple items visible
<CarouselItem className="md:basis-1/2 lg:basis-1/3">

// Autoplay (use embla-carousel-autoplay)
<Carousel plugins={[Autoplay({ delay: 3000 })]}>

// Dots navigation
// Custom implementation needed
```

**Accessibility**:

- Pause autoplay on hover/focus
- Keyboard navigation
- Live region for slide changes

**Refs**:

- shadcn Carousel: https://ui.shadcn.com/docs/components/carousel
- Embla Carousel: https://www.embla-carousel.com/

---

## Image

**Purpose**: Optimized, responsive images with loading states.

**When to use**: Any image display.

**Usual contents**: Image with alt text.

**Structure**:

```tsx
import Image from "next/image";

{
  /* Fixed dimensions */
}
<Image src="/image.jpg" alt="Description" width={800} height={600} className="rounded-lg" />;

{
  /* Fill container */
}
<div className="relative aspect-video">
  <Image src="/image.jpg" alt="Description" fill className="object-cover rounded-lg" />
</div>;

{
  /* With blur placeholder */
}
<Image
  src="/image.jpg"
  alt="Description"
  width={800}
  height={600}
  placeholder="blur"
  blurDataURL="data:image/jpeg;base64,..."
/>;
```

**Accessibility**:

- Always include meaningful `alt` text
- Decorative images: `alt=""`

**Refs**:

- Next.js Image: https://nextjs.org/docs/app/api-reference/components/image

---

## Video

**Purpose**: Embedded video content.

**When to use**: Product demos, background videos, tutorials.

**Usual contents**: Video element or embed iframe.

**Structure**:

```tsx
{
  /* Native video */
}
<video className="aspect-video w-full rounded-lg" controls poster="/poster.jpg">
  <source src="/video.mp4" type="video/mp4" />
</video>;

{
  /* YouTube embed */
}
<div className="aspect-video">
  <iframe
    className="h-full w-full rounded-lg"
    src="https://www.youtube.com/embed/VIDEO_ID"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowFullScreen
  />
</div>;

{
  /* Background video (muted, autoplay) */
}
<video className="absolute inset-0 h-full w-full object-cover" autoPlay muted loop playsInline>
  <source src="/bg-video.mp4" type="video/mp4" />
</video>;
```

**Accessibility**:

- Include captions/transcripts
- `prefers-reduced-motion` check for autoplay

---

## Code Block

**Purpose**: Display formatted code with syntax highlighting.

**When to use**: Documentation, tutorials, API references.

**Usual contents**: Code snippet with language indicator.

**Structure**:

```tsx
// Using a syntax highlighter like shiki or prism
<pre className="overflow-x-auto rounded-lg bg-muted p-4">
  <code className="text-sm">{codeString}</code>
</pre>

// With copy button
<div className="relative">
  <pre className="overflow-x-auto rounded-lg bg-muted p-4 pr-12">
    <code>{codeString}</code>
  </pre>
  <Button
    size="icon"
    variant="ghost"
    className="absolute right-2 top-2"
    onClick={() => copyToClipboard(codeString)}
  >
    <Copy className="h-4 w-4" />
  </Button>
</div>

// With language label
<div className="rounded-lg border">
  <div className="flex items-center justify-between border-b bg-muted px-4 py-2">
    <span className="text-sm text-muted-foreground">typescript</span>
    <CopyButton />
  </div>
  <pre className="overflow-x-auto p-4">
    <code>{codeString}</code>
  </pre>
</div>
```

**Accessibility**:

- Use `<pre>` and `<code>` semantically
- Ensure sufficient contrast

## Blockquote

**Purpose**: Highlight quoted text, testimonials, or citations.

**When to use**: Quotes, testimonials, citations, callouts.

**Structure**:

```tsx
<blockquote className="border-l-4 border-primary pl-6 py-2 italic">
  <p className="text-lg text-muted-foreground">
    "The best way to predict the future is to invent it."
  </p>
  <footer className="mt-2 text-sm font-medium">— Alan Kay</footer>
</blockquote>
```

**Variants**:

```tsx
// Large quote
<blockquote className="border-l-4 border-primary pl-6 py-4">
  <p className="text-2xl font-light italic text-foreground">
    "Design is not just what it looks like and feels like."
  </p>
  <footer className="mt-4 text-sm font-medium text-muted-foreground">
    — Steve Jobs
  </footer>
</blockquote>

// Centered with quote marks
<blockquote className="relative text-center px-8">
  <span className="absolute top-0 left-0 text-6xl text-primary/20">"</span>
  <p className="text-xl italic relative z-10">
    {quote.text}
  </p>
  <footer className="mt-4 text-sm font-medium">
    — {quote.author}
  </footer>
</blockquote>

// With avatar
<blockquote className="border-l-4 border-primary pl-6">
  <p className="text-lg italic">"{text}"</p>
  <footer className="mt-4 flex items-center gap-3">
    <Avatar src={author.avatar} name={author.name} />
    <div>
      <div className="font-medium">{author.name}</div>
      <div className="text-sm text-muted-foreground">{author.title}</div>
    </div>
  </footer>
</blockquote>
```

**Accessibility**:

- Use `<blockquote>` element
- Include `<footer>` for attribution
- Add `cite` attribute if referencing a URL

---

## Empty State

**Purpose**: Display when no data exists or an action is needed.

**When to use**: Empty lists, first-time use, error states, success states.

**Structure**:

```tsx
<div className="flex flex-col items-center justify-center py-12 text-center">
  {/* Icon */}
  <div className="h-12 w-12 rounded-full bg-muted flex items-center justify-center mb-4">
    <Inbox className="h-6 w-6 text-muted-foreground" />
  </div>

  {/* Title */}
  <h3 className="text-lg font-semibold">No tasks yet</h3>

  {/* Description */}
  <p className="text-sm text-muted-foreground mt-1 max-w-sm">
    Get started by creating your first task.
  </p>

  {/* Action */}
  <Button className="mt-4">
    <Plus className="mr-2 h-4 w-4" />
    Create Task
  </Button>
</div>
```

**Variants**:
| Variant | Icon | Use Case |
|---------|------|----------|
| `empty` | Inbox/Box | No data |
| `search` | Search | No results |
| `error` | AlertTriangle | Error state |
| `success` | CheckCircle | Completed |
| `loading` | Loader | Loading |

**In a container**:

```tsx
<div className="border rounded-lg p-8">
  <div className="flex flex-col items-center text-center">
    <Search className="h-10 w-10 text-muted-foreground mb-4" />
    <h3 className="font-semibold">No results found</h3>
    <p className="text-sm text-muted-foreground mt-1">Try adjusting your search or filters.</p>
    <Button variant="outline" className="mt-4">
      Clear Filters
    </Button>
  </div>
</div>
```

**Accessibility**:

- Use appropriate heading level
- Ensure sufficient color contrast
- Provide clear next action

---

## Prose / Typography

**Purpose**: Styled article/content text with proper typography.

**When to use**: Blog posts, documentation, long-form content.

**Structure**:

```tsx
<article className="prose prose-slate dark:prose-invert max-w-none">
  <h1>Article Title</h1>
  <p className="lead">Introduction paragraph with larger text...</p>
  <h2>Section Heading</h2>
  <p>
    Body text with <strong>bold</strong> and <em>italic</em>...
  </p>
  <ul>
    <li>List item one</li>
    <li>List item two</li>
  </ul>
  <blockquote>Quoted text...</blockquote>
  <pre>
    <code>Code block...</code>
  </pre>
</article>
```

**Tailwind Typography plugin**:

```bash
npm install -D @tailwindcss/typography
```

```js
// tailwind.config.js
module.exports = {
  plugins: [require("@tailwindcss/typography")],
};
```

**Customizing**:

```tsx
<article className={cn(
  "prose prose-slate dark:prose-invert",
  "prose-headings:font-bold prose-headings:text-foreground",
  "prose-a:text-primary prose-a:no-underline hover:prose-a:underline",
  "prose-code:text-pink-500 prose-code:bg-muted prose-code:px-1 prose-code:rounded",
  "prose-pre:bg-muted prose-pre:border",
  "max-w-none"
)}>
```

**Variants**:
| Size | Class | Use Case |
|------|-------|----------|
| `sm` | `prose-sm` | Compact |
| `default` | `prose` | Standard |
| `lg` | `prose-lg` | Comfortable |
| `xl` | `prose-xl` | Editorial |

**Accessibility**:

- Proper heading hierarchy (h1 → h2 → h3)
- Sufficient line height (1.5-1.7)
- Max-width for readability (65ch)

**Refs**:

- Tailwind Typography: https://tailwindcss.com/docs/typography-plugin

---

## Figure / Caption

**Purpose**: Image with associated caption text.

**When to use**: Article images, diagrams, charts with descriptions.

**Structure**:

```tsx
<figure className="my-8">
  <img src="/diagram.png" alt="System architecture diagram" className="rounded-lg border" />
  <figcaption className="mt-3 text-sm text-center text-muted-foreground">
    Figure 1: System architecture showing data flow between services
  </figcaption>
</figure>
```

**Variants**:

```tsx
// Full-width with caption
<figure className="my-8">
  <div className="relative aspect-video rounded-lg overflow-hidden">
    <Image src="/photo.jpg" alt="Description" fill className="object-cover" />
  </div>
  <figcaption className="mt-3 flex items-center gap-2 text-sm text-muted-foreground">
    <Info className="h-4 w-4" />
    <span>Photo by Photographer Name on Unsplash</span>
  </figcaption>
</figure>

// Side-by-side (image + caption)
<figure className="flex gap-6 items-start my-8">
  <img src="/chart.png" alt="Chart" className="w-2/3 rounded-lg" />
  <figcaption className="w-1/3 text-sm">
    <strong>Figure 2:</strong> Quarterly revenue growth showing 25% increase
    compared to last year.
  </figcaption>
</figure>
```

**Accessibility**:

- Use `<figure>` and `<figcaption>` elements
- Alt text describes image content
- Caption provides context

---

## Divider / Separator

**Purpose**: Visual separation between content sections.

**When to use**: Between sections, list items, thematic breaks.

**Structure**:

```tsx
// Simple horizontal rule
<hr className="my-8 border-border" />

// With text
<div className="relative my-8">
  <div className="absolute inset-0 flex items-center">
    <span className="w-full border-t" />
  </div>
  <div className="relative flex justify-center text-xs uppercase">
    <span className="bg-background px-2 text-muted-foreground">
      Continue Reading
    </span>
  </div>
</div>
```

**Variants**:

```tsx
// Dotted
<hr className="my-8 border-dotted border-border" />

// Gradient
<hr className="my-8 h-px bg-gradient-to-r from-transparent via-border to-transparent" />

// Vertical (in flex container)
<div className="flex items-center gap-4">
  <span>Left content</span>
  <div className="h-4 w-px bg-border" />
  <span>Right content</span>
</div>
```

**Accessibility**:

- Use `<hr>` for thematic breaks
- Ensure sufficient contrast
- Don't use purely decorative dividers for content separation
