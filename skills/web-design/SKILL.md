---
name: web-design
description: Index for web design skills - routing table for UI/UX work
---

# Web Design Skills Index

This is the routing index for web design work. Load specific sub-skills based on the task.

## Quick Reference

| Task                   | Skill to Load           | Components/Topics                           |
| ---------------------- | ----------------------- | ------------------------------------------- |
| New project setup      | `design-system`         | Tokens, colors, typography, Tailwind config |
| Existing project audit | `design-system`         | Analyze & extend existing setup             |
| Page structure         | `components-layout`     | Container, Grid, Section, Stack, Sidebar    |
| Navigation             | `components-navigation` | Navbar, Sidebar, Tabs, Breadcrumbs, Footer  |
| Content display        | `components-content`    | Hero, Card, Avatar, Badge, Testimonial      |
| Forms & inputs         | `components-forms`      | Input, Select, Checkbox, DatePicker, Form   |
| User feedback          | `components-feedback`   | Button, Alert, Toast, Modal, Tooltip        |
| Data display           | `components-data`       | Table, List, Accordion, Stepper             |
| Marketing pages        | `components-marketing`  | Pricing, CTA, FAQ, Newsletter               |
| Full pages             | `page-templates`        | Landing, Dashboard, Auth, Blog              |
| Motion & polish        | `animations`            | Entrances, micro-interactions, transitions  |
| Component docs         | `storybook`             | Setup, stories, visual testing              |

## Existing Project Checklist

Before building in an existing project, check for:

```
□ tailwind.config.ts/js    → Existing theme tokens?
□ globals.css              → CSS variables defined?
□ components/ui/           → shadcn components installed?
□ lib/utils.ts             → cn() helper present?
□ .storybook/              → Storybook configured?
□ package.json             → Check installed dependencies
```

If these exist, **analyze before building**:

1. Extract existing color tokens
2. Identify typography scale in use
3. Note spacing patterns
4. Match existing component styles
5. Extend rather than replace

## New Project Checklist

For fresh projects, establish in order:

1. **Design System** → `/design-system` command
   - Discovery questions
   - Color palette
   - Typography scale
   - Spacing tokens
   - Tailwind config
   - CSS variables

2. **Core Components** → Install shadcn/ui base
   - Button, Input, Card (essentials)
   - Customize to match design system

3. **Layout** → Build page structure
   - Container, Section, Grid
   - Navigation shell

4. **Pages** → Implement full pages
   - Use established components
   - Maintain consistency

5. **Polish** → Add animations, refine
   - Micro-interactions
   - Page transitions
   - Loading states

## Component Count by Skill

Counts below are based on current `##` sections in each file.

| Skill                   | Count   | Key Components                                                                      |
| ----------------------- | ------- | ----------------------------------------------------------------------------------- |
| `components-layout`     | 14      | Container, Section, Grid, Stack, Sidebar Layout, Split Layout, Sticky Header        |
| `components-navigation` | 15      | Navbar, Mobile Nav, Sidebar, Breadcrumbs, Tabs, Pagination, Footer, Command Palette |
| `components-content`    | 17      | Hero, Card, Feature Card, Avatar, Badge, Stats, Testimonial, Timeline, Carousel     |
| `components-forms`      | 15      | Input, Textarea, Select, Checkbox, Radio Group, Switch, Slider, Form, Wizard        |
| `components-feedback`   | 16      | Button, Alert, Toast, Dialog, Alert Dialog, Sheet, Drawer, Tooltip, Progress        |
| `components-data`       | 12      | Table, Data Table, List, Accordion, Tree View, Stepper, Scroll Area, Empty State    |
| `components-marketing`  | 14      | Pricing Card, Pricing Table, CTA Section, FAQ, Newsletter, Logo Cloud, Banner       |
| **Total**               | **103** |                                                                                     |

## Reference Links

- **shadcn/ui**: https://ui.shadcn.com/docs/components
- **Radix Primitives**: https://www.radix-ui.com/primitives
- **Tailwind CSS**: https://tailwindcss.com/docs
- **Framer Motion**: https://www.framer.com/motion/
- **Lucide Icons**: https://lucide.dev/icons
- **WAI-ARIA Patterns**: https://www.w3.org/WAI/ARIA/apg/patterns/

## Using context7

For latest docs, use context7 MCP:

```
use context7 to look up [shadcn Button component]
use context7 to look up [Tailwind grid utilities]
use context7 to look up [Framer Motion variants]
```
