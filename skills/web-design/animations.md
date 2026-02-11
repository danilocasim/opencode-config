---
name: animations
description: Framer Motion and Tailwind animation patterns
---

# Animations & Motion

Animation principles using Framer Motion and Tailwind.

---

## Tailwind Built-in Animations

### Transition Utilities

```tsx
// Fade
<Fade in className="opacity-0 opacity-100 duration-300" />

// Scale
<Scale className="scale-95 scale-100 duration-300" />

// Slide
<Slide in className="-translate-x-full translate-x-0 duration-300" />
```

### Custom Keyframes

```css
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
@keyframes slideIn {
  from {
    transform: translateX(-100%);
  }
  to {
    transform: translateX(0);
  }
}
```

---

## Framer Motion Patterns

### Entrance Animations

#### Fade In

```tsx
import { motion, AnimatePresence } from "framer-motion";

<Fade in initial={{ opacity: 0 }} animate={{ opacity: 1 }} transition={{ duration: 0.3 }} />;
```

**Variants**:
| Variant | Values |
|---------|---------|
| Fade | opacity: 0 → 1 |
| Fade Up | opacity: 0, y: 20 → 0 |
| Fade Down | opacity: 0, y: -20 → 0 |
| Scale In | scale: 0.95 → 1 |

---

#### Slide In

```tsx
<motion.div
  initial={{ x: "-100%" }}
  animate={{ x: 0 }}
  transition={{ type: "spring", stiffness: 300, damping: 30 }}
/>
```

**Variants**:
| Variant | Axis |
|---------|-------|
| Slide Left | x: -100% → 0 |
| Slide Right | x: 100% → 0 |
| Slide Up | y: 20 → 0 |
| Slide Down | y: -20 → 0 |

---

#### Staggered Children

```tsx
<motion.ul
  initial="hidden"
  whileInView="visible"
  viewport={{ once: true, margin: "-100px" }}
  variants={{
    hidden: { opacity: 0 },
    visible: {
      opacity: 1,
      transition: {
        staggerChildren: 0.1,
      },
    },
  }}
>
  {items.map((item, i) => (
    <motion.li key={i}>{item}</motion.li>
  ))}
</motion.ul>
```

**Use cases**: Lists, grids, feature cards

---

### Layout Animations

#### Accordion/Collapse

```tsx
<AnimatePresence>
  {isOpen && (
    <motion.section
      initial={{ height: 0, opacity: 0 }}
      animate={{ height: "auto", opacity: 1 }}
      exit={{ height: 0, opacity: 0 }}
    >
      {content}
    </motion.section>
  )}
</AnimatePresence>
```

#### Tab Switch

```tsx
<motion.div
  layoutId={tabId}
  initial={{ opacity: 0 }}
  animate={{ opacity: 1 }}
  transition={{ duration: 0.2 }}
/>
```

---

### Micro-interactions

#### Button Hover

```tsx
<motion.button whileHover={{ scale: 1.05 }} whileTap={{ scale: 0.95 }} />
```

#### Focus Rings

```tsx
<motion.input focus={{ boxShadow: "0 0 0 3px rgba(primary, 0.2)" }} />
```

#### Hover Cards

```tsx
<motion.div
  whileHover={{ y: -4, scale: 1.02 }}
  transition={{ type: "spring", stiffness: 400, damping: 30 }}
/>
```

---

### Page Transitions (Next.js App Router)

```tsx
"use client";

import { motion, AnimatePresence } from "framer-motion";
import { useRouter } from "next/navigation";

export function PageTransition({ children }) {
  const router = useRouter();

  return (
    <AnimatePresence mode="wait" initial={false}>
      <motion.div
        initial={{ opacity: 0, y: 20 }}
        animate={{ opacity: 1, y: 0 }}
        exit={{ opacity: 0, y: -20 }}
        transition={{
          type: "spring",
          stiffness: 260,
          damping: 20,
        }}
      >
        {children}
      </motion.div>
    </AnimatePresence>
  );
}
```

---

## Scroll-triggered Animations

### While In View

```tsx
import { useInView } from "framer-motion";

function AnimatedSection({ children }) {
  const ref = useRef(null);
  const isInView = useInView(ref, { once: false, amount: 0.3 });

  return (
    <motion.section
      ref={ref}
      initial={{ opacity: 0 }}
      animate={isInView ? { opacity: 1, y: 0 } : { opacity: 0, y: 50 }}
      transition={{ duration: 0.6 }}
    >
      {children}
    </motion.section>
  );
}
```

### Scroll Progress

```tsx
import { useScroll } from "framer-motion";

function ScrollProgress() {
  const { scrollYProgress } = useScroll();

  return (
    <motion.div
      className="fixed top-0 left-0 right-0 h-1 bg-primary"
      style={{ scaleX: scrollYProgress }}
    />
  );
}
```

---

## Loading States

### Skeleton Loading

```tsx
<motion.div
  animate={{ opacity: [0.4, 0.8, 1] }}
  transition={{ duration: 0.5, repeat: Infinity }}
  className="h-4 w-32 rounded bg-muted"
/>
```

### Pulse Loading

```tsx
<motion.div
  animate={{
    scale: [1, 1, 1, 1],
    opacity: [1, 0.8, 0.6, 1],
  }}
  transition={{ duration: 1.5, repeat: Infinity }}
/>
```

### Spinner

```tsx
<motion.div
  animate={{ rotate: 360 }}
  transition={{ duration: 1, repeat: Infinity, ease: "linear" }}
/>
```

---

## Reduced Motion (Accessibility)

Check user's motion preference:

```tsx
function useReducedMotion() {
  const [prefersReduced, setPrefersReduced] = useState(false);

  useEffect(() => {
    const mediaQuery = window.matchMedia("(prefers-reduced-motion: reduce)");
    setPrefersReduced(mediaQuery.matches);
  }, []);

  return prefersReduced;
}

// Apply to animations
const duration = useReducedMotion() ? 0 : 0.3;
```

---

## Performance Tips

1. Use `layout` prop for layout animations (GPU accelated)
2. Use GPU for transforms (will-change: transform)
3. Avoid animating height/width when possible
4. Use `transform` instead of top/left properties
5. Limit concurrent animations
6. Use `AnimatePresence` sparingly

---

## Best Practices

1. **Keep it subtle** - Don't distract from content
2. **Consistent easing** - Use same spring values
3. **Respect preferences** - Check `prefers-reduced-motion`
4. **Test on low-end devices** - Animations can be slow
5. **Consider `layout`** - For page transitions and layout changes

---

## References

- **Framer Motion**: https://www.framer.com/motion/
- **Motion Library**: https://motion.dev/
- **Web Animations API**: https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API

---

## ✅ Complete
