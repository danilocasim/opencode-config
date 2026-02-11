---
name: components-marketing
description: Marketing components - Pricing, CTA, FAQ, Newsletter, Social proof
---

# Marketing Components

Components for landing pages, marketing sites, and conversion.

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

## Pricing Card

**Purpose**: Display a pricing tier/plan.

**When to use**: Pricing pages, plan comparison.

**Usual contents**: Plan name, price, billing period, feature list, CTA button.

**Variants**:
| Variant | Description |
|---------|-------------|
| Simple | Basic card with features |
| Highlighted | "Popular" or "Recommended" badge |
| Enterprise | "Contact us" instead of price |
| With toggle | Monthly/annual switch affects price |

**Best practices**:

- Highlight recommended plan visually
- Show savings on annual plans
- Limit to 3-4 plans for easy comparison
- Most important features at top of list

---

## Pricing Table

**Purpose**: Side-by-side plan comparison.

**When to use**: Detailed feature comparison across plans.

**Usual contents**: Feature rows, plan columns, checkmarks/x marks, CTAs.

**Features**:

- Sticky header row on scroll
- Feature grouping by category
- Tooltips for feature explanations
- Mobile: Convert to stacked cards

**Best practices**:

- Group related features together
- Use checkmarks (✓) and dashes (—) not ✗
- Highlight differences, not similarities

---

## CTA Section

**Purpose**: Drive user action (signup, demo, download).

**When to use**: Between content sections, end of pages.

**Usual contents**: Headline, subtext, button(s), optional background.

**Variants**:
| Variant | Style |
|---------|-------|
| Simple | Text + single button |
| Split | Text left, form right |
| Centered | All content centered |
| Full-width | Edge-to-edge background |
| With image | Background image/gradient |

**Best practices**:

- One clear action (or primary + secondary)
- Urgent, benefit-focused headline
- Contrasting background to stand out

---

## FAQ

**Purpose**: Answer common questions.

**When to use**: Product pages, pricing pages, support sections.

**Usual contents**: Question/answer pairs in accordion format.

**Variants**:
| Variant | Layout |
|---------|--------|
| Single column | Questions stacked |
| Two column | Questions split into columns |
| Categorized | Grouped by topic with tabs |
| Searchable | Filter questions by keyword |

**Best practices**:

- Most common questions first
- Keep answers concise
- Link to detailed docs for complex topics
- Include contact option for unanswered questions

---

## Newsletter

**Purpose**: Collect email signups.

**When to use**: Footers, dedicated sections, popups.

**Usual contents**: Headline, description, email input, submit button.

**Variants**:
| Variant | Layout |
|---------|--------|
| Inline | Input + button in row |
| Stacked | Input above button |
| Card | Contained in a card |
| With incentive | "Get 10% off" messaging |

**Best practices**:

- Clear value proposition (what they'll receive)
- Privacy reassurance ("We won't spam")
- Single field (email only) reduces friction
- Success state confirmation

---

## Logo Cloud

**Purpose**: Display partner/client/press logos for credibility.

**When to use**: Landing pages, about pages, trust building.

**Usual contents**: Logo images in a row or grid.

**Variants**:
| Variant | Behavior |
|---------|----------|
| Static | Fixed logo display |
| Scrolling | Infinite horizontal scroll |
| Grid | Multi-row layout |
| Grayscale | Muted logos, color on hover |

**Best practices**:

- Consistent logo sizing/spacing
- Grayscale keeps focus on content
- "Trusted by" or "Featured in" heading
- 4-6 logos is optimal

---

## Comparison Table

**Purpose**: Compare product vs competitors or features.

**When to use**: Product pages, decision-making contexts.

**Usual contents**: Feature rows, product columns, checkmarks/values.

**Variants**:
| Variant | Use Case |
|---------|----------|
| Us vs Them | Product vs generic competitor |
| Named competitors | Specific competitor comparison |
| Before/After | Old way vs new way |

**Best practices**:

- Highlight your advantages prominently
- Be honest about limitations
- Use your brand column as reference point (first or center)

---

## Banner

**Purpose**: Prominent announcement or promotion.

**When to use**: Site-wide announcements, promotions, alerts.

**Usual contents**: Message, optional link/CTA, dismiss button.

**Variants**:
| Variant | Position |
|---------|----------|
| Top bar | Above navbar, full width |
| Floating | Bottom of viewport |
| Inline | Within content area |

**Best practices**:

- Keep message short (one line)
- Make dismissible (respect user choice)
- Don't overuse (banner blindness)
- Time-sensitive content (expiration dates)

---

## Social Share

**Purpose**: Enable content sharing on social platforms.

**When to use**: Blog posts, product pages, achievements.

**Usual contents**: Platform icons/buttons, optional share count.

**Platforms**: Twitter/X, Facebook, LinkedIn, Reddit, Email, Copy link.

**Variants**:
| Variant | Style |
|---------|-------|
| Icons only | Compact, icon buttons |
| With labels | Icon + platform name |
| Floating | Fixed position sidebar |
| Inline | Within content flow |

**Best practices**:

- Pre-fill share text when possible
- Include only relevant platforms
- Copy link as universal fallback

---

## Cookie Consent

**Purpose**: GDPR/privacy compliance for cookie usage.

**When to use**: All sites using cookies/tracking (legally required in EU).

**Usual contents**: Message, accept/reject buttons, preferences link.

**Variants**:
| Variant | Complexity |
|---------|------------|
| Simple | Accept/Reject only |
| Detailed | Category toggles (necessary, analytics, marketing) |
| Banner | Bottom/top bar |
| Modal | Centered overlay |

**Best practices**:

- Don't use dark patterns (reject should be equally visible)
- Remember user preference
- Link to full privacy policy
- Allow preference changes later

---

## Testimonial Grid

**Purpose**: Multiple testimonials in grid layout.

**When to use**: Social proof sections, case study pages.

**Usual contents**: Quote cards with attribution.

**Variants**:
| Variant | Layout |
|---------|--------|
| Grid | 2-3 columns |
| Masonry | Variable height cards |
| Carousel | Sliding testimonials |
| Featured | One large + several small |

**Best practices**:

- Mix of personas/industries
- Include company logos when possible
- Real names and photos increase trust
- Video testimonials are most powerful

## Feature List

**Purpose**: Showcase product features with icons and descriptions.

**When to use**: Product pages, feature sections, landing pages.

**Structure**:

```tsx
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
  {features.map((feature) => (
    <div key={feature.id} className="flex gap-4">
      <div className="flex-shrink-0">
        <div className="h-12 w-12 rounded-lg bg-primary/10 flex items-center justify-center">
          <feature.icon className="h-6 w-6 text-primary" />
        </div>
      </div>
      <div>
        <h3 className="font-semibold">{feature.title}</h3>
        <p className="text-sm text-muted-foreground mt-1">{feature.description}</p>
      </div>
    </div>
  ))}
</div>
```

**Variants**:

```tsx
// With checkmarks
<div className="space-y-4">
  {features.map(feature => (
    <div key={feature.id} className="flex gap-3">
      <Check className="h-5 w-5 text-green-500 flex-shrink-0" />
      <div>
        <h4 className="font-medium">{feature.title}</h4>
        <p className="text-sm text-muted-foreground">{feature.description}</p>
      </div>
    </div>
  ))}
</div>

// Grid with large icons
<div className="grid grid-cols-2 md:grid-cols-4 gap-8 text-center">
  {features.map(feature => (
    <div key={feature.id}>
      <feature.icon className="h-12 w-12 mx-auto text-primary" />
      <h3 className="mt-4 font-semibold">{feature.title}</h3>
    </div>
  ))}
</div>
```

---

## Stats Counter

**Purpose**: Display impressive numbers with animation.

**When to use**: Social proof, landing pages, about pages.

**Structure**:

```tsx
function AnimatedCounter({ value, suffix = "" }: CounterProps) {
  const [count, setCount] = useState(0);
  const ref = useRef<HTMLSpanElement>(null);
  const isInView = useInView(ref, { once: true });

  useEffect(() => {
    if (isInView) {
      const duration = 2000;
      const steps = 60;
      const increment = value / steps;
      let current = 0;

      const timer = setInterval(() => {
        current += increment;
        if (current >= value) {
          setCount(value);
          clearInterval(timer);
        } else {
          setCount(Math.floor(current));
        }
      }, duration / steps);

      return () => clearInterval(timer);
    }
  }, [isInView, value]);

  return (
    <span ref={ref} className="tabular-nums">
      {count.toLocaleString()}
      {suffix}
    </span>
  );
}

// Usage
<div className="grid grid-cols-2 md:grid-cols-4 gap-8">
  {stats.map((stat) => (
    <div key={stat.label} className="text-center">
      <div className="text-3xl md:text-4xl font-bold">
        <AnimatedCounter value={stat.value} suffix={stat.suffix} />
      </div>
      <div className="text-sm text-muted-foreground mt-1">{stat.label}</div>
    </div>
  ))}
</div>;
```

**Accessibility**:

- Provide static values for screen readers
- Don't autoplay if user prefers reduced motion
- Ensure numbers are readable

---

## Integration Grid

**Purpose**: Show third-party integrations or partners.

**When to use**: Integration pages, partner showcases, ecosystem pages.

**Structure**:

```tsx
<div className="grid grid-cols-2 md:grid-cols-4 lg:grid-cols-6 gap-6">
  {integrations.map((integration) => (
    <a
      key={integration.id}
      href={integration.url}
      className="group flex flex-col items-center p-4 rounded-lg border hover:border-primary transition-colors"
    >
      <img src={integration.logo} alt={integration.name} className="h-12 w-12 object-contain" />
      <span className="mt-2 text-sm font-medium">{integration.name}</span>
      <span className="text-xs text-muted-foreground">{integration.category}</span>
    </a>
  ))}
</div>
```

**Accessibility**:

- Meaningful alt text for logos
- Clear hover/focus states
- Consider grayscale until hover
