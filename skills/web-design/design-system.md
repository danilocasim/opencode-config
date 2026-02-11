---
name: design-system
description: Design system creation, tokens, theming, and Tailwind configuration
---

# Design System Skill

Complete guide for establishing or extending a design system.

---

## Discovery Questions (New Projects)

Ask these to establish design direction:

### 1. Project Context

- What is this project? (SaaS, e-commerce, portfolio, blog, internal tool, agency site)
- Who is the target audience? (developers, enterprises, consumers, creative professionals)
- What problem does it solve?
- Any existing brand guidelines, logos, or assets?

### 2. Aesthetic Direction

- What mood/feeling should it evoke? (minimal, bold, playful, professional, luxurious, techy)
- Any reference sites or products you admire? (provide 2-3 examples)
- Light mode only, dark mode only, or both?
- Any specific visual elements? (gradients, glassmorphism, illustrations, photography)

### 3. Typography

- Preferred font pairing? Or should I suggest based on aesthetic?
- Any requirements? (multilingual support, monospace for code, specific weights)
- Preference for serif, sans-serif, or mixed?

### 4. Color

- Primary brand color? (hex code or description)
- Any secondary colors?
- Colors to avoid?
- Specific meaning for semantic colors? (what should "success" or "warning" feel like)

### 5. Technical

- Using shadcn/ui? (strongly recommended)
- Existing Tailwind config to extend?
- Animation preference? (subtle, moderate, expressive, none)
- Icon library preference? (Lucide recommended)

### 6. Scope

- What pages are planned? (landing, dashboard, auth, settings, etc.)
- Mobile-first or desktop-first priority?
- Expected complexity? (simple marketing site vs complex app)

---

## Existing Project Audit

For existing projects, analyze before extending:

### Step 1: Check Configuration Files

```bash
# Look for these files:
tailwind.config.ts    # or .js
globals.css           # or app/globals.css
components/ui/        # shadcn components
lib/utils.ts          # cn() helper
```

### Step 2: Extract Existing Tokens

From `tailwind.config.ts`:

```ts
// Look for theme.extend.colors, theme.extend.fontFamily, etc.
```

From `globals.css`:

```css
/* Look for :root { --background: ...; --foreground: ...; } */
```

### Step 3: Document Current State

- List all custom colors defined
- Note typography scale in use
- Identify spacing patterns (consistent or arbitrary?)
- Catalog existing components
- Note any inconsistencies to fix

### Step 4: Plan Extensions

- What's missing from the design system?
- What's inconsistent that should be unified?
- What new tokens are needed?
- How to add without breaking existing styles?

---

## Spacing Scale

Use Tailwind's default scale based on 4px (0.25rem) units:

| Token | Size     | Pixels | Use Case                    |
| ----- | -------- | ------ | --------------------------- |
| `0`   | 0        | 0px    | Reset                       |
| `px`  | 1px      | 1px    | Borders                     |
| `0.5` | 0.125rem | 2px    | Micro spacing               |
| `1`   | 0.25rem  | 4px    | Tight spacing               |
| `1.5` | 0.375rem | 6px    | -                           |
| `2`   | 0.5rem   | 8px    | Component padding (sm)      |
| `3`   | 0.75rem  | 12px   | -                           |
| `4`   | 1rem     | 16px   | Component padding (default) |
| `5`   | 1.25rem  | 20px   | -                           |
| `6`   | 1.5rem   | 24px   | Component padding (lg)      |
| `8`   | 2rem     | 32px   | Section spacing (sm)        |
| `10`  | 2.5rem   | 40px   | -                           |
| `12`  | 3rem     | 48px   | Section spacing (md)        |
| `16`  | 4rem     | 64px   | Section spacing (lg)        |
| `20`  | 5rem     | 80px   | Hero spacing                |
| `24`  | 6rem     | 96px   | Major section breaks        |

### Spacing Guidelines

- **Consistent increments**: Use scale values, avoid arbitrary numbers
- **Component internal**: 2-6 (8-24px)
- **Between components**: 4-8 (16-32px)
- **Between sections**: 12-24 (48-96px)
- **Mobile**: Reduce by ~25% on smaller screens

---

## Typography Scale

### Font Sizes

| Token  | Size            | Line Height | Use Case                 |
| ------ | --------------- | ----------- | ------------------------ |
| `xs`   | 0.75rem (12px)  | 1rem        | Captions, labels         |
| `sm`   | 0.875rem (14px) | 1.25rem     | Secondary text, metadata |
| `base` | 1rem (16px)     | 1.5rem      | Body text (default)      |
| `lg`   | 1.125rem (18px) | 1.75rem     | Lead paragraphs          |
| `xl`   | 1.25rem (20px)  | 1.75rem     | H4, card titles          |
| `2xl`  | 1.5rem (24px)   | 2rem        | H3                       |
| `3xl`  | 1.875rem (30px) | 2.25rem     | H2                       |
| `4xl`  | 2.25rem (36px)  | 2.5rem      | H1, section titles       |
| `5xl`  | 3rem (48px)     | 1           | Display, hero headlines  |
| `6xl`  | 3.75rem (60px)  | 1           | Large display            |
| `7xl`  | 4.5rem (72px)   | 1           | Extra large display      |

### Font Weights

| Token      | Weight | Use Case                           |
| ---------- | ------ | ---------------------------------- |
| `light`    | 300    | De-emphasized text (use sparingly) |
| `normal`   | 400    | Body text                          |
| `medium`   | 500    | Emphasis, labels                   |
| `semibold` | 600    | Headings, buttons                  |
| `bold`     | 700    | Strong emphasis                    |

### Font Pairings (Recommendations)

| Style       | Headings          | Body              | Vibe                   |
| ----------- | ----------------- | ----------------- | ---------------------- |
| Modern Sans | Inter             | Inter             | Clean, versatile       |
| Technical   | Geist             | Geist             | Developer-focused      |
| Editorial   | Playfair Display  | Source Sans Pro   | Elegant, editorial     |
| Startup     | Cal Sans          | Inter             | Bold, contemporary     |
| Corporate   | Plus Jakarta Sans | Plus Jakarta Sans | Professional           |
| Playful     | Outfit            | Nunito            | Friendly, approachable |

### Typography CSS Variables

```css
:root {
  --font-sans: "Inter", ui-sans-serif, system-ui, sans-serif;
  --font-mono: "JetBrains Mono", ui-monospace, monospace;
  /* Optional: heading font if different */
  --font-heading: var(--font-sans);
}
```

---

## Color System

### Semantic Color Tokens (shadcn convention)

```css
:root {
  /* Backgrounds */
  --background: 0 0% 100%; /* Page background */
  --foreground: 222.2 84% 4.9%; /* Default text */

  /* Cards & elevated surfaces */
  --card: 0 0% 100%;
  --card-foreground: 222.2 84% 4.9%;

  /* Popovers, dropdowns */
  --popover: 0 0% 100%;
  --popover-foreground: 222.2 84% 4.9%;

  /* Primary action color */
  --primary: 222.2 47.4% 11.2%;
  --primary-foreground: 210 40% 98%;

  /* Secondary/muted actions */
  --secondary: 210 40% 96.1%;
  --secondary-foreground: 222.2 47.4% 11.2%;

  /* Muted backgrounds & text */
  --muted: 210 40% 96.1%;
  --muted-foreground: 215.4 16.3% 46.9%;

  /* Accent highlights */
  --accent: 210 40% 96.1%;
  --accent-foreground: 222.2 47.4% 11.2%;

  /* Destructive actions */
  --destructive: 0 84.2% 60.2%;
  --destructive-foreground: 210 40% 98%;

  /* Borders & inputs */
  --border: 214.3 31.8% 91.4%;
  --input: 214.3 31.8% 91.4%;
  --ring: 222.2 84% 4.9%;

  /* Border radius */
  --radius: 0.5rem;
}

.dark {
  --background: 222.2 84% 4.9%;
  --foreground: 210 40% 98%;
  /* ... dark mode values */
}
```

### Creating a Color Palette

1. **Start with primary**: Your brand color
2. **Generate shades**: 50-950 scale using tools like:
   - https://uicolors.app/create
   - https://www.tailwindshades.com/
3. **Add semantic colors**: Success (green), warning (amber), error (red), info (blue)
4. **Test contrast**: Ensure WCAG AA compliance (4.5:1 for text)

### Color Guidelines

- **Primary**: Main CTAs, links, active states
- **Secondary**: Secondary buttons, subtle backgrounds
- **Muted**: Disabled states, placeholder text
- **Accent**: Highlights, badges, focus rings
- **Destructive**: Delete actions, errors

---

## Shadows & Elevation

```css
:root {
  --shadow-sm: 0 1px 2px 0 rgb(0 0 0 / 0.05);
  --shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1);
  --shadow-md: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
  --shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
  --shadow-xl: 0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1);
}
```

| Level | Token       | Use Case                          |
| ----- | ----------- | --------------------------------- |
| 0     | none        | Flat elements                     |
| 1     | `shadow-sm` | Subtle lift (inputs, small cards) |
| 2     | `shadow`    | Default elevation (cards)         |
| 3     | `shadow-md` | Hover states, dropdowns           |
| 4     | `shadow-lg` | Modals, popovers                  |
| 5     | `shadow-xl` | Large modals, drawers             |

---

## Border Radius Scale

```css
:root {
  --radius: 0.5rem; /* Base radius */
}
```

| Token          | Value                     | Use Case              |
| -------------- | ------------------------- | --------------------- |
| `rounded-none` | 0                         | Sharp corners         |
| `rounded-sm`   | 0.125rem                  | Subtle rounding       |
| `rounded`      | 0.25rem                   | Small elements        |
| `rounded-md`   | calc(var(--radius) - 2px) | Inputs, small buttons |
| `rounded-lg`   | var(--radius)             | Cards, large buttons  |
| `rounded-xl`   | calc(var(--radius) + 4px) | Large cards           |
| `rounded-2xl`  | 1rem                      | Panels, modals        |
| `rounded-full` | 9999px                    | Pills, avatars        |

---

## Output Templates

### 1. tailwind.config.ts

```ts
import type { Config } from "tailwindcss";

const config: Config = {
  darkMode: ["class"],
  content: ["./pages/**/*.{ts,tsx}", "./components/**/*.{ts,tsx}", "./app/**/*.{ts,tsx}"],
  theme: {
    container: {
      center: true,
      padding: "2rem",
      screens: {
        "2xl": "1400px",
      },
    },
    extend: {
      colors: {
        border: "hsl(var(--border))",
        input: "hsl(var(--input))",
        ring: "hsl(var(--ring))",
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        primary: {
          DEFAULT: "hsl(var(--primary))",
          foreground: "hsl(var(--primary-foreground))",
        },
        secondary: {
          DEFAULT: "hsl(var(--secondary))",
          foreground: "hsl(var(--secondary-foreground))",
        },
        destructive: {
          DEFAULT: "hsl(var(--destructive))",
          foreground: "hsl(var(--destructive-foreground))",
        },
        muted: {
          DEFAULT: "hsl(var(--muted))",
          foreground: "hsl(var(--muted-foreground))",
        },
        accent: {
          DEFAULT: "hsl(var(--accent))",
          foreground: "hsl(var(--accent-foreground))",
        },
        popover: {
          DEFAULT: "hsl(var(--popover))",
          foreground: "hsl(var(--popover-foreground))",
        },
        card: {
          DEFAULT: "hsl(var(--card))",
          foreground: "hsl(var(--card-foreground))",
        },
      },
      borderRadius: {
        lg: "var(--radius)",
        md: "calc(var(--radius) - 2px)",
        sm: "calc(var(--radius) - 4px)",
      },
      fontFamily: {
        sans: ["var(--font-sans)", "ui-sans-serif", "system-ui", "sans-serif"],
        mono: ["var(--font-mono)", "ui-monospace", "monospace"],
      },
      keyframes: {
        "accordion-down": {
          from: { height: "0" },
          to: { height: "var(--radix-accordion-content-height)" },
        },
        "accordion-up": {
          from: { height: "var(--radix-accordion-content-height)" },
          to: { height: "0" },
        },
      },
      animation: {
        "accordion-down": "accordion-down 0.2s ease-out",
        "accordion-up": "accordion-up 0.2s ease-out",
      },
    },
  },
  plugins: [require("tailwindcss-animate")],
};

export default config;
```

### 2. globals.css

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  :root {
    --background: 0 0% 100%;
    --foreground: 222.2 84% 4.9%;
    --card: 0 0% 100%;
    --card-foreground: 222.2 84% 4.9%;
    --popover: 0 0% 100%;
    --popover-foreground: 222.2 84% 4.9%;
    --primary: 222.2 47.4% 11.2%;
    --primary-foreground: 210 40% 98%;
    --secondary: 210 40% 96.1%;
    --secondary-foreground: 222.2 47.4% 11.2%;
    --muted: 210 40% 96.1%;
    --muted-foreground: 215.4 16.3% 46.9%;
    --accent: 210 40% 96.1%;
    --accent-foreground: 222.2 47.4% 11.2%;
    --destructive: 0 84.2% 60.2%;
    --destructive-foreground: 210 40% 98%;
    --border: 214.3 31.8% 91.4%;
    --input: 214.3 31.8% 91.4%;
    --ring: 222.2 84% 4.9%;
    --radius: 0.5rem;
  }

  .dark {
    --background: 222.2 84% 4.9%;
    --foreground: 210 40% 98%;
    --card: 222.2 84% 4.9%;
    --card-foreground: 210 40% 98%;
    --popover: 222.2 84% 4.9%;
    --popover-foreground: 210 40% 98%;
    --primary: 210 40% 98%;
    --primary-foreground: 222.2 47.4% 11.2%;
    --secondary: 217.2 32.6% 17.5%;
    --secondary-foreground: 210 40% 98%;
    --muted: 217.2 32.6% 17.5%;
    --muted-foreground: 215 20.2% 65.1%;
    --accent: 217.2 32.6% 17.5%;
    --accent-foreground: 210 40% 98%;
    --destructive: 0 62.8% 30.6%;
    --destructive-foreground: 210 40% 98%;
    --border: 217.2 32.6% 17.5%;
    --input: 217.2 32.6% 17.5%;
    --ring: 212.7 26.8% 83.9%;
  }
}

@layer base {
  * {
    @apply border-border;
  }
  body {
    @apply bg-background text-foreground;
  }
}
```

### 3. Theme Provider Setup

```tsx
// components/theme-provider.tsx
"use client";

import * as React from "react";
import { ThemeProvider as NextThemesProvider } from "next-themes";
import { type ThemeProviderProps } from "next-themes/dist/types";

export function ThemeProvider({ children, ...props }: ThemeProviderProps) {
  return <NextThemesProvider {...props}>{children}</NextThemesProvider>;
}

// In app/layout.tsx:
// <ThemeProvider attribute="class" defaultTheme="system" enableSystem>
//   {children}
// </ThemeProvider>
```

### 4. design-tokens.md (Documentation)

```markdown
# Design Tokens

## Colors

| Token        | Light     | Dark      | Usage           |
| ------------ | --------- | --------- | --------------- |
| `background` | white     | slate-950 | Page background |
| `foreground` | slate-900 | slate-50  | Primary text    |
| `primary`    | brand-600 | brand-400 | CTAs, links     |
| ...          |           |           |                 |

## Typography

| Scale   | Size    | Weight   | Usage          |
| ------- | ------- | -------- | -------------- |
| Display | 5xl-7xl | bold     | Hero headlines |
| H1      | 4xl     | semibold | Page titles    |
| ...     |         |          |                |

## Spacing

Use Tailwind scale. Key values:

- Component padding: 4 (16px)
- Section gap: 16 (64px)
- ...
```

---

## Storybook Design System Documentation

```tsx
// stories/DesignSystem.mdx
import { Meta, ColorPalette, ColorItem, Typeset } from '@storybook/blocks';

<Meta title="Design System/Overview" />

# Design System

## Colors

<ColorPalette>
  <ColorItem
    title="Primary"
    subtitle="Brand color"
    colors={{ Default: 'hsl(222.2 47.4% 11.2%)' }}
  />
  {/* Add more colors */}
</ColorPalette>

## Typography

<Typeset
  fontSizes={['12px', '14px', '16px', '18px', '24px', '36px']}
  fontWeight={400}
  sampleText="The quick brown fox jumps over the lazy dog"
  fontFamily="Inter, sans-serif"
/>
```

---

## Reference Links

- **shadcn/ui Theming**: https://ui.shadcn.com/docs/theming
- **Tailwind Config**: https://tailwindcss.com/docs/configuration
- **HSL Colors**: https://www.w3schools.com/colors/colors_hsl.asp
- **WCAG Contrast**: https://webaim.org/resources/contrastchecker/
- **Color Palette Generator**: https://uicolors.app/create
