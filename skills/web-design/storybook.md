---
name: storybook
description: Storybook setup, story patterns, and documentation
---

# Storybook

Setup and patterns for documenting React components with Storybook.

---

## Setup

### Next.js + Storybook 8

```bash
npx storybook@latest init --type nextjs
```

### Essential Addons

Install these for full functionality:

```bash
npx storybook@latest add @storybook/addon-essentials
npx storybook@latest add @storybook/addon-a11y
npx storybook@latest add @storybook/addon-viewport
npx storybook@latest add @storybook/addon-themes
```

### Folder Structure

```
.storybook/
├── main.ts                    # Entry point
├── preview.ts                 # Global decorators
├── manager.ts                 # Storybook manager
└── stories/
    ├── Introduction.stories.mdx   # Documentation
    └── components/
        └── Button.stories.tsx  # Component stories
```

---

## Story Structure (CSF3)

### Basic Pattern

```tsx
import type { Meta, StoryObj } from "@storybook/react";

import { Button } from "./button";

const meta: Meta<typeof Button> = {
  title: "Components/Button",
  component: Button,
  tags: ["autodocs"],
};

export default meta;
type Story = StoryObj<typeof Button>;

export const Default: Story = {
  args: {
    children: "Button",
  },
};
```

### With Controls

```tsx
const meta: Meta<typeof Button> = {
  title: "Components/Button",
  component: Button,
  parameters: {
    layout: "centered",
  },
};

export default meta;
type Story = StoryObj<typeof Button>;

export const Primary: Story = {
  args: {
    variant: "primary",
    children: "Primary",
  },
};

export const AllVariants: Story = {
  render: () => (
    <div className="flex gap-4">
      <Button variant="default">Default</Button>
      <Button variant="secondary">Secondary</Button>
      <Button variant="outline">Outline</Button>
      <Button variant="ghost">Ghost</Button>
    </div>
  ),
};
```

### ArgTypes Definition

```tsx
const meta: Meta<typeof Button> = {
  title: "Components/Button",
  component: Button,
  argTypes: {
    variant: {
      control: "select",
      options: ["default", "secondary", "outline", "ghost", "destructive"],
      description: "Button variant",
    },
    size: {
      control: "select",
      options: ["sm", "default", "lg"],
      description: "Button size",
    },
  },
};
```

---

## Story Types

### Default Story

Primary usage example.

### All Variants Story

Show all visual variants together.

### Interactive Story

Demonstrates component behavior with controls.

### Playground Story

All controls available for experimentation.

### Responsive Story

Shows component at different viewport sizes.

### Edge Cases Story

Tests boundary conditions, error states.

---

## Documentation (MDX)

### Meta Fields

```tsx
const meta: Meta<typeof Component> = {
  title: "ComponentName",
  subtitle: "Brief description",
  component: Component,
  tags: ["category", "another-category"],
};
```

### Description Block

```tsx
export default function ComponentName() {
  return (
    <>
      <Meta of={meta} />
      <Story name="Introduction">
        <p>Detailed description of what this component does and when to use it.</p>
      </Story>
    </>
  );
}
```

### Example Code

````tsx
<Story name="Examples">
  <Canvas>
    <ComponentExample />
  </Canvas>
  <Raw>```tsx // Your code here ```</Raw>
</Story>
````

---

## Organization

### Naming Conventions

- Folder name matches component: `components/button/`
- File name matches component: `Button.stories.tsx`
- Story names: PascalCase with clear descriptions

### Tagging Strategy

| Tag                   | Purpose           |
| --------------------- | ----------------- |
| `category:ui`         | UI components     |
| `category:forms`      | Form components   |
| `category:data`       | Data display      |
| `category:layout`     | Layout components |
| `category:navigation` | Navigation        |
| `category:marketing`  | Marketing         |

---

## Auto-Docs

### Component Description

Generated from JSDoc comments in your component:

```tsx
/**
 * Button component for primary actions.
 *
 * @param variant - Visual style of the button
 * @param size - Size of the button
 * @param icon - Optional icon to display
 * @param disabled - Whether the button is disabled
 * @param loading - Whether to show loading state
 * @param children - Button content
 */
```

### Props Table

Generated from TypeScript interfaces:

```tsx
<ArgsTable of={Button} />
```

---

## Visual Testing (Chromatic)

### Snapshot Testing

Storybook captures visual output on every story run to detect changes.

### Workflow

1. Configure Chromatic with build script
2. Run Storybook build
3. Visual changes appear in Chromatic UI
4. Review and approve/reject

### Best Practices

1. Test all variants
2. Include edge cases
3. Test with dark/light themes
4. Document changes in PRs

---

## Existing Project Integration

### Install in Existing Project

```bash
npx storybook@latest init
```

### Migration Guide

1. Create `.storybook/main.ts`
2. Configure `.storybook/preview.ts` with theme
3. Move/create stories in `src/components/**/stories.mdx`
4. Update scripts in `package.json`

---

## Best Practices

1. **One story per file** for simple components
2. **Group stories** for complex components
3. **Use MDX** for long documentation
4. **Include edge cases** and error states
5. **Maintain consistency** with project's styling
6. **Update docs** when component changes

---

## References

- **Storybook Docs**: https://storybook.js.org/docs
- **React Storybook**: https://storybook.js.org/docs/react/get-started/introduction
- **MDX**: https://mdxjs.com/
- **Chromatic**: https://www.chromatic.com/docs
