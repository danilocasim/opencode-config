---
name: page-templates
description: Full page templates - Landing, Dashboard, Auth, Blog, E-commerce
---

# Page Templates

Common page structures and section flows.

---

## Landing Page

**Purpose**: Convert visitors to users/customers.

**Typical section flow**:

1. **Hero** - Headline, value prop, CTA, visual
2. **Logo cloud** - Social proof (trusted by)
3. **Features** - 3-6 key benefits/features
4. **How it works** - 3-step process explanation
5. **Testimonials** - Customer quotes
6. **Pricing** - Plan options (optional)
7. **FAQ** - Common questions
8. **CTA** - Final conversion push
9. **Footer** - Links, legal, social

**Key components**: Hero, Feature Card, Testimonial, Pricing Card, FAQ, CTA Section, Footer

**Layout considerations**:

- Full-width sections with contained content
- Alternating backgrounds for visual rhythm
- Mobile: Stack everything vertically
- Clear visual hierarchy guiding to CTAs

**Best practices**:

- One primary CTA per section
- Social proof early (builds trust)
- Address objections (FAQ, guarantees)
- Fast loading (above-fold content priority)

---

## Dashboard

**Purpose**: Application main interface for data and actions.

**Typical structure**:

```
┌─────────────────────────────────────────┐
│ Header (breadcrumbs, search, user menu) │
├──────────┬──────────────────────────────┤
│          │ Stats cards row              │
│ Sidebar  ├──────────────────────────────┤
│ (nav)    │ Main content area            │
│          │ (tables, charts, cards)      │
│          │                              │
└──────────┴──────────────────────────────┘
```

**Key components**: Sidebar, Navbar, Stats Card, Data Table, Card, Tabs

**Layout considerations**:

- Sidebar: Fixed or collapsible (icon-only on collapse)
- Mobile: Sidebar becomes drawer/sheet
- Main area: Scrollable, header can be sticky
- Dense information display

**Best practices**:

- Most important data visible first
- Quick actions easily accessible
- Clear navigation hierarchy
- Loading states for async data

---

## Settings Page

**Purpose**: User/account configuration.

**Typical structure**:

```
┌────────────────────────────────────────┐
│ Page header (Settings)                 │
├──────────┬─────────────────────────────┤
│ Settings │ Form sections               │
│ nav      │ - Profile                   │
│ (tabs or │ - Notifications             │
│ sidebar) │ - Security                  │
│          │ - Billing                   │
│          │                             │
│          │ [Save Changes]              │
└──────────┴─────────────────────────────┘
```

**Key components**: Tabs/Sidebar nav, Form, Input, Switch, Select, Button

**Layout considerations**:

- Vertical tabs/sidebar for many categories
- Horizontal tabs for few categories
- Form sections with clear headings
- Sticky save button or per-section save

**Best practices**:

- Group related settings
- Explain what each setting does
- Show current state clearly
- Confirm destructive actions

---

## Auth Pages (Login/Signup)

**Purpose**: User authentication.

**Typical structure**:

```
┌─────────────────────────────────────────┐
│                                         │
│         ┌─────────────────┐             │
│         │ Logo            │             │
│         │ Title           │             │
│         │ Form            │             │
│         │ - Email         │             │
│         │ - Password      │             │
│         │ [Submit]        │             │
│         │ Social auth     │             │
│         │ Links           │             │
│         └─────────────────┘             │
│                                         │
└─────────────────────────────────────────┘
```

**Variants**:
| Variant | Layout |
|---------|--------|
| Centered card | Card in center of page |
| Split | Form left, image/branding right |
| Full-page form | No card, form fills space |

**Key components**: Card, Form, Input, Button, Separator ("or"), Social buttons

**Layout considerations**:

- Minimal distractions (no full nav)
- Mobile: Full-width card or no card
- Clear path between login/signup
- Password visibility toggle

**Best practices**:

- Social login options (Google, GitHub, etc.)
- "Forgot password" link visible
- Show password requirements on signup
- Clear error messages inline

---

## Blog / Article Page

**Purpose**: Long-form content consumption.

**Typical structure**:

```
┌─────────────────────────────────────────┐
│ Header (nav)                            │
├─────────────────────────────────────────┤
│ Article header                          │
│ - Title                                 │
│ - Author, date, read time               │
│ - Featured image                        │
├─────────────────────────────────────────┤
│ Article content (prose)                 │
│ - Max-width for readability             │
│ - Typography optimized                  │
├─────────────────────────────────────────┤
│ Author bio                              │
├─────────────────────────────────────────┤
│ Related articles                        │
├─────────────────────────────────────────┤
│ Footer                                  │
└─────────────────────────────────────────┘
```

**Key components**: Avatar, Badge (tags), Prose styling, Card (related), Social Share

**Layout considerations**:

- Max content width: 65-75 characters per line
- Generous line height (1.6-1.8)
- Optional: Table of contents sidebar
- Mobile: Full-width with padding

**Best practices**:

- Reading time estimate
- Progress indicator (optional)
- Share buttons (floating or end)
- Related content for engagement

---

## E-commerce Product Page

**Purpose**: Product information and purchase conversion.

**Typical structure**:

```
┌─────────────────────────────────────────┐
│ Header (nav, cart)                      │
├─────────────────────────────────────────┤
│ Breadcrumbs                             │
├───────────────────┬─────────────────────┤
│ Product images    │ Product info        │
│ - Gallery         │ - Title             │
│ - Zoom            │ - Price             │
│ - Thumbnails      │ - Variants          │
│                   │ - Add to cart       │
│                   │ - Description       │
├───────────────────┴─────────────────────┤
│ Product details tabs                    │
│ (Description, Specs, Reviews)           │
├─────────────────────────────────────────┤
│ Related products                        │
├─────────────────────────────────────────┤
│ Footer                                  │
└─────────────────────────────────────────┘
```

**Key components**: Image gallery, Select (variants), Button, Tabs, Card, Badge (sale)

**Layout considerations**:

- Images: Large, zoomable, multiple angles
- Sticky add-to-cart on mobile
- Reviews prominently displayed
- Trust badges near purchase button

**Best practices**:

- High-quality images (multiple angles)
- Clear pricing (show savings if on sale)
- Stock status visible
- Easy variant selection
- Social proof (reviews, ratings)
- Trust signals (returns, shipping, security)

---

## 404 / Error Page

**Purpose**: Handle navigation errors gracefully.

**Typical contents**:

- Clear error message
- Illustration or icon
- Explanation of what happened
- Links to navigate away (home, search, popular pages)

**Best practices**:

- Friendly, not technical language
- Helpful navigation options
- Consistent with site branding
- Search box if applicable

---

## Settings Page (Implementation Example)

**Purpose**: Configure application preferences and account settings.

**Typical structure**:

```
Settings/
├── Sidebar Navigation
│   ├── Profile
│   ├── Account
│   ├── Notifications
│   ├── Appearance
│   ├── Billing
│   └── Security
└── Content Area
    └── Settings Form
```

**Key sections**:

1. **Profile** - Name, avatar, bio, public info
2. **Account** - Email, password, delete account
3. **Notifications** - Email, push, in-app preferences
4. **Appearance** - Theme, language, density
5. **Billing** - Payment methods, invoices, plan
6. **Security** - 2FA, sessions, API keys

**Structure**:

```tsx
export default function SettingsPage() {
  return (
    <div className="container py-6">
      <div className="flex flex-col lg:flex-row gap-8">
        {/* Sidebar */}
        <aside className="lg:w-64">
          <nav className="space-y-1">
            <a href="#profile" className="flex items-center px-3 py-2 rounded-md bg-muted">
              <User className="mr-3 h-4 w-4" />
              Profile
            </a>
            <a href="#account" className="flex items-center px-3 py-2 rounded-md hover:bg-muted">
              <Settings className="mr-3 h-4 w-4" />
              Account
            </a>
            {/* More nav items */}
          </nav>
        </aside>

        {/* Main content */}
        <main className="flex-1 max-w-2xl">
          <Card>
            <CardHeader>
              <CardTitle>Profile</CardTitle>
              <CardDescription>
                Manage your public profile information
              </CardDescription>
            </CardHeader>
            <CardContent className="space-y-4">
              <div className="flex items-center gap-4">
                <Avatar className="h-20 w-20">
                  <AvatarImage src={user.avatar} />
                  <AvatarFallback>{user.initials}</AvatarFallback>
                </Avatar>
                <Button variant="outline">Change Avatar</Button>
              </div>

              <div className="grid gap-4">
                <div className="grid grid-cols-2 gap-4">
                  <FormField name="firstName" ... />
                  <FormField name="lastName" ... />
                </div>
                <FormField name="bio" ... />
              </div>
            </CardContent>
            <CardFooter className="flex justify-end gap-2">
              <Button variant="outline">Cancel</Button>
              <Button>Save Changes</Button>
            </CardFooter>
          </Card>
        </main>
      </div>
    </div>
  )
}
```

**Layout considerations**:

- Sticky sidebar navigation
- Clear section headings
- Auto-save or prominent save button
- Confirmation for destructive actions

---

## Profile Page

**Purpose**: Display user information and activity.

**Typical structure**:

1. **Header** - Cover photo, avatar, name, actions
2. **Stats** - Followers, following, posts
3. **Bio** - Description, location, links
4. **Content tabs** - Posts, activity, media, likes

**Structure**:

```tsx
export default function ProfilePage() {
  return (
    <div>
      {/* Cover image */}
      <div className="h-48 bg-gradient-to-r from-blue-500 to-purple-600" />

      <div className="container -mt-16">
        <div className="flex flex-col md:flex-row gap-6">
          {/* Avatar */}
          <Avatar className="h-32 w-32 border-4 border-background">
            <AvatarImage src={user.avatar} />
            <AvatarFallback className="text-2xl">{user.initials}</AvatarFallback>
          </Avatar>

          {/* Info */}
          <div className="flex-1">
            <div className="flex flex-col md:flex-row md:items-center justify-between gap-4">
              <div>
                <h1 className="text-2xl font-bold">{user.name}</h1>
                <p className="text-muted-foreground">@{user.handle}</p>
              </div>
              <div className="flex gap-2">
                <Button variant="outline">Edit Profile</Button>
                <Button>Follow</Button>
              </div>
            </div>

            {/* Bio */}
            <p className="mt-4">{user.bio}</p>

            {/* Meta */}
            <div className="flex flex-wrap gap-4 mt-4 text-sm text-muted-foreground">
              <span className="flex items-center gap-1">
                <MapPin className="h-4 w-4" />
                {user.location}
              </span>
              <span className="flex items-center gap-1">
                <LinkIcon className="h-4 w-4" />
                <a href={user.website}>{user.website}</a>
              </span>
              <span className="flex items-center gap-1">
                <Calendar className="h-4 w-4" />
                Joined {user.joinedDate}
              </span>
            </div>

            {/* Stats */}
            <div className="flex gap-6 mt-4">
              <div>
                <span className="font-bold">{user.following}</span>
                <span className="text-muted-foreground ml-1">Following</span>
              </div>
              <div>
                <span className="font-bold">{user.followers}</span>
                <span className="text-muted-foreground ml-1">Followers</span>
              </div>
            </div>
          </div>
        </div>

        {/* Tabs */}
        <Tabs defaultValue="posts" className="mt-8">
          <TabsList>
            <TabsTrigger value="posts">Posts</TabsTrigger>
            <TabsTrigger value="replies">Replies</TabsTrigger>
            <TabsTrigger value="media">Media</TabsTrigger>
            <TabsTrigger value="likes">Likes</TabsTrigger>
          </TabsList>
          <TabsContent value="posts" className="mt-6">
            <PostGrid posts={posts} />
          </TabsContent>
          {/* Other tabs */}
        </Tabs>
      </div>
    </div>
  );
}
```

**Layout considerations**:

- Responsive avatar positioning
- Clear visual hierarchy
- Consistent spacing
- Mobile-optimized stats display

---

## Documentation Page

**Purpose**: Technical documentation with navigation.

**Typical structure**:

```
Docs/
├── Sticky Header (search, version selector)
├── Left Sidebar (table of contents)
├── Main Content (article)
└── Right Sidebar (on-page nav)
```

**Key components**:

1. **Search** - Full-text documentation search
2. **Version selector** - Switch between versions
3. **Table of contents** - Hierarchical navigation
4. **Breadcrumbs** - Show current location
5. **On-page navigation** - Anchor links to headings
6. **Code blocks** - Syntax highlighted examples
7. **Callouts** - Info, warning, tip boxes

**Structure**:

```tsx
export default function DocsPage() {
  return (
    <div className="flex min-h-screen">
      {/* Left sidebar */}
      <aside className="hidden lg:block w-64 border-r sticky top-14 h-[calc(100vh-3.5rem)] overflow-y-auto">
        <nav className="p-4 space-y-6">
          {sections.map((section) => (
            <div key={section.title}>
              <h4 className="font-semibold mb-2">{section.title}</h4>
              <ul className="space-y-1">
                {section.pages.map((page) => (
                  <li key={page.href}>
                    <a
                      href={page.href}
                      className={cn(
                        "block px-2 py-1 text-sm rounded",
                        isActive(page.href)
                          ? "bg-primary/10 text-primary font-medium"
                          : "text-muted-foreground hover:text-foreground"
                      )}
                    >
                      {page.title}
                    </a>
                  </li>
                ))}
              </ul>
            </div>
          ))}
        </nav>
      </aside>

      {/* Main content */}
      <main className="flex-1 min-w-0">
        <article className="prose prose-slate dark:prose-invert max-w-3xl mx-auto px-4 py-8">
          <h1>{doc.title}</h1>
          <p className="lead">{doc.description}</p>

          {doc.content}

          {/* Pagination */}
          <div className="flex justify-between mt-12 pt-6 border-t">
            {doc.prev && (
              <a href={doc.prev.href} className="flex flex-col">
                <span className="text-sm text-muted-foreground">Previous</span>
                <span className="font-medium">{doc.prev.title}</span>
              </a>
            )}
            {doc.next && (
              <a href={doc.next.href} className="flex flex-col items-end">
                <span className="text-sm text-muted-foreground">Next</span>
                <span className="font-medium">{doc.next.title}</span>
              </a>
            )}
          </div>
        </article>
      </main>

      {/* Right sidebar */}
      <aside className="hidden xl:block w-64 sticky top-14 h-[calc(100vh-3.5rem)] overflow-y-auto">
        <nav className="p-4">
          <h4 className="font-semibold text-sm mb-2">On this page</h4>
          <ul className="space-y-1">
            {headings.map((heading) => (
              <li key={heading.id}>
                <a
                  href={`#${heading.id}`}
                  className={cn(
                    "block text-sm py-1",
                    heading.level === 2 ? "" : "pl-4",
                    isActive(heading.id)
                      ? "text-primary font-medium"
                      : "text-muted-foreground hover:text-foreground"
                  )}
                >
                  {heading.text}
                </a>
              </li>
            ))}
          </ul>
        </nav>
      </aside>
    </div>
  );
}
```

**Layout considerations**:

- Sticky navigation
- Collapsible sidebar on mobile
- Search integration
- Code copy buttons
- Linkable headings
