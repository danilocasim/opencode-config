---
name: components-feedback
description: Feedback components - Button, Alert, Toast, Modal, Tooltip, Progress
---

# Feedback Components

Components for user actions and system feedback.

---

## Button

**Purpose**: Primary action trigger.

**When to use**: Forms, CTAs, actions, navigation triggers.

**Usual contents**: Label, optional icon.

**Structure**:
```tsx
import { Button } from "@/components/ui/button"

<Button>Default</Button>
<Button variant="secondary">Secondary</Button>
<Button variant="outline">Outline</Button>
<Button variant="ghost">Ghost</Button>
<Button variant="link">Link</Button>
<Button variant="destructive">Destructive</Button>
```

**Variants**:
| Variant | Use Case |
|---------|----------|
| default | Primary actions |
| secondary | Secondary actions |
| outline | Tertiary actions, cancel |
| ghost | Subtle actions, icon buttons |
| link | Inline text actions |
| destructive | Delete, dangerous actions |

**Sizes**:
```tsx
<Button size="sm">Small</Button>
<Button size="default">Default</Button>
<Button size="lg">Large</Button>
<Button size="icon">
  <Search className="h-4 w-4" />
</Button>
```

**With icon**:
```tsx
<Button>
  <Mail className="mr-2 h-4 w-4" />
  Login with Email
</Button>

<Button>
  Continue
  <ArrowRight className="ml-2 h-4 w-4" />
</Button>
```

**Loading state**:
```tsx
<Button disabled>
  <Loader2 className="mr-2 h-4 w-4 animate-spin" />
  Please wait
</Button>
```

**As link**:
```tsx
<Button asChild>
  <Link href="/dashboard">Go to Dashboard</Link>
</Button>
```

**Accessibility**:
- Use semantic `<button>` (default)
- `aria-label` for icon-only buttons
- Disabled state visible and announced

**Refs**:
- shadcn Button: https://ui.shadcn.com/docs/components/button

---

## Alert

**Purpose**: Inline contextual messages.

**When to use**: Form validation, status messages, warnings.

**Usual contents**: Icon, title, description.

**Structure**:
```tsx
import { Alert, AlertDescription, AlertTitle } from "@/components/ui/alert"

<Alert>
  <Terminal className="h-4 w-4" />
  <AlertTitle>Heads up!</AlertTitle>
  <AlertDescription>
    You can add components to your app using the CLI.
  </AlertDescription>
</Alert>
```

**Variants**:
```tsx
// Default (info)
<Alert>...</Alert>

// Destructive (error/warning)
<Alert variant="destructive">
  <AlertCircle className="h-4 w-4" />
  <AlertTitle>Error</AlertTitle>
  <AlertDescription>Something went wrong.</AlertDescription>
</Alert>

// Success (custom styling)
<Alert className="border-green-500/50 text-green-500 [&>svg]:text-green-500">
  <CheckCircle className="h-4 w-4" />
  <AlertTitle>Success</AlertTitle>
  <AlertDescription>Your changes have been saved.</AlertDescription>
</Alert>
```

**Dismissible**:
```tsx
const [visible, setVisible] = useState(true)

{visible && (
  <Alert className="relative">
    <AlertTitle>Notice</AlertTitle>
    <AlertDescription>This is dismissible.</AlertDescription>
    <Button 
      variant="ghost" 
      size="icon" 
      className="absolute right-2 top-2 h-6 w-6"
      onClick={() => setVisible(false)}
    >
      <X className="h-4 w-4" />
    </Button>
  </Alert>
)}
```

**Accessibility**:
- Use `role="alert"` for important messages
- Icon should be decorative (`aria-hidden`)

**Refs**:
- shadcn Alert: https://ui.shadcn.com/docs/components/alert

---

## Toast

**Purpose**: Temporary notification messages.

**When to use**: Action confirmations, errors, status updates.

**Usual contents**: Title, description, optional action button.

**Structure**:
```tsx
// In component
import { useToast } from "@/components/ui/use-toast"

const { toast } = useToast()

<Button onClick={() => toast({ title: "Saved", description: "Your changes have been saved." })}>
  Save
</Button>

// In layout (required)
import { Toaster } from "@/components/ui/toaster"

<Toaster />
```

**Variants**:
```tsx
// Default
toast({ title: "Success", description: "Operation completed." })

// Destructive
toast({ variant: "destructive", title: "Error", description: "Something went wrong." })

// With action
toast({
  title: "File deleted",
  description: "The file has been moved to trash.",
  action: <ToastAction altText="Undo">Undo</ToastAction>,
})
```

**Positioning** (in Toaster):
```tsx
<Toaster position="top-right" /> // top-left, top-center, bottom-left, bottom-center, bottom-right
```

**Accessibility**:
- Auto-announced by screen readers
- Dismissible with close button
- Action buttons focusable

**Refs**:
- shadcn Toast: https://ui.shadcn.com/docs/components/toast
- Sonner (alternative): https://sonner.emilkowal.ski/

---

## Dialog / Modal

**Purpose**: Overlay content requiring user attention/action.

**When to use**: Confirmations, forms, detail views, settings.

**Usual contents**: Title, description, content, action buttons.

**Structure**:
```tsx
import {
  Dialog,
  DialogContent,
  DialogDescription,
  DialogFooter,
  DialogHeader,
  DialogTitle,
  DialogTrigger,
} from "@/components/ui/dialog"

<Dialog>
  <DialogTrigger asChild>
    <Button>Open Dialog</Button>
  </DialogTrigger>
  <DialogContent className="sm:max-w-[425px]">
    <DialogHeader>
      <DialogTitle>Edit Profile</DialogTitle>
      <DialogDescription>
        Make changes to your profile here. Click save when done.
      </DialogDescription>
    </DialogHeader>
    <div className="py-4">
      {/* Form content */}
    </div>
    <DialogFooter>
      <Button type="submit">Save changes</Button>
    </DialogFooter>
  </DialogContent>
</Dialog>
```

**Sizes**:
```tsx
<DialogContent className="sm:max-w-sm">   // Small
<DialogContent className="sm:max-w-md">   // Medium
<DialogContent className="sm:max-w-lg">   // Large
<DialogContent className="sm:max-w-xl">   // Extra large
<DialogContent className="sm:max-w-4xl">  // Full width
```

**Controlled**:
```tsx
const [open, setOpen] = useState(false)

<Dialog open={open} onOpenChange={setOpen}>
  {/* ... */}
</Dialog>
```

**Accessibility**:
- Focus trapped inside
- Close on Escape
- `aria-labelledby` and `aria-describedby` automatic

**Refs**:
- shadcn Dialog: https://ui.shadcn.com/docs/components/dialog

---

## Alert Dialog

**Purpose**: Confirmation dialog for destructive/important actions.

**When to use**: Delete confirmations, irreversible actions.

**Usual contents**: Title, description, cancel and confirm buttons.

**Structure**:
```tsx
import {
  AlertDialog,
  AlertDialogAction,
  AlertDialogCancel,
  AlertDialogContent,
  AlertDialogDescription,
  AlertDialogFooter,
  AlertDialogHeader,
  AlertDialogTitle,
  AlertDialogTrigger,
} from "@/components/ui/alert-dialog"

<AlertDialog>
  <AlertDialogTrigger asChild>
    <Button variant="destructive">Delete Account</Button>
  </AlertDialogTrigger>
  <AlertDialogContent>
    <AlertDialogHeader>
      <AlertDialogTitle>Are you absolutely sure?</AlertDialogTitle>
      <AlertDialogDescription>
        This action cannot be undone. This will permanently delete your
        account and remove your data from our servers.
      </AlertDialogDescription>
    </AlertDialogHeader>
    <AlertDialogFooter>
      <AlertDialogCancel>Cancel</AlertDialogCancel>
      <AlertDialogAction className="bg-destructive text-destructive-foreground hover:bg-destructive/90">
        Delete
      </AlertDialogAction>
    </AlertDialogFooter>
  </AlertDialogContent>
</AlertDialog>
```

**Accessibility**:
- Cannot be dismissed by clicking outside
- Forces user to make explicit choice

**Refs**:
- shadcn Alert Dialog: https://ui.shadcn.com/docs/components/alert-dialog

---

## Sheet

**Purpose**: Side panel overlay.

**When to use**: Mobile navigation, filters, detail panels.

**Usual contents**: Header, scrollable content, optional footer.

**Structure**:
```tsx
import {
  Sheet,
  SheetContent,
  SheetDescription,
  SheetHeader,
  SheetTitle,
  SheetTrigger,
} from "@/components/ui/sheet"

<Sheet>
  <SheetTrigger asChild>
    <Button variant="outline">Open Sheet</Button>
  </SheetTrigger>
  <SheetContent>
    <SheetHeader>
      <SheetTitle>Edit Profile</SheetTitle>
      <SheetDescription>Make changes to your profile.</SheetDescription>
    </SheetHeader>
    <div className="py-4">
      {/* Content */}
    </div>
  </SheetContent>
</Sheet>
```

**Sides**:
```tsx
<SheetContent side="right"> // default
<SheetContent side="left">
<SheetContent side="top">
<SheetContent side="bottom">
```

**Sizes**:
```tsx
<SheetContent className="w-[400px] sm:w-[540px]">
<SheetContent className="sm:max-w-lg">
```

**Refs**:
- shadcn Sheet: https://ui.shadcn.com/docs/components/sheet

---

## Drawer

**Purpose**: Bottom sheet on mobile, dialog on desktop.

**When to use**: Responsive overlays, mobile-friendly modals.

**Usual contents**: Same as Sheet/Dialog.

**Structure**:
```tsx
import {
  Drawer,
  DrawerContent,
  DrawerDescription,
  DrawerHeader,
  DrawerTitle,
  DrawerTrigger,
} from "@/components/ui/drawer"

<Drawer>
  <DrawerTrigger asChild>
    <Button>Open Drawer</Button>
  </DrawerTrigger>
  <DrawerContent>
    <DrawerHeader>
      <DrawerTitle>Drawer Title</DrawerTitle>
      <DrawerDescription>Drawer description.</DrawerDescription>
    </DrawerHeader>
    <div className="p-4">
      {/* Content */}
    </div>
  </DrawerContent>
</Drawer>
```

**Refs**:
- shadcn Drawer: https://ui.shadcn.com/docs/components/drawer
- Vaul: https://vaul.emilkowal.ski/

---

## Tooltip

**Purpose**: Brief contextual info on hover/focus.

**When to use**: Icon buttons, truncated text, additional context.

**Usual contents**: Short text (1-2 sentences max).

**Structure**:
```tsx
import {
  Tooltip,
  TooltipContent,
  TooltipProvider,
  TooltipTrigger,
} from "@/components/ui/tooltip"

<TooltipProvider>
  <Tooltip>
    <TooltipTrigger asChild>
      <Button variant="ghost" size="icon">
        <Settings className="h-4 w-4" />
      </Button>
    </TooltipTrigger>
    <TooltipContent>
      <p>Settings</p>
    </TooltipContent>
  </Tooltip>
</TooltipProvider>
```

**Positioning**:
```tsx
<TooltipContent side="top">    // default
<TooltipContent side="right">
<TooltipContent side="bottom">
<TooltipContent side="left">
```

**Accessibility**:
- Shows on focus for keyboard users
- Short delay before showing

**Refs**:
- shadcn Tooltip: https://ui.shadcn.com/docs/components/tooltip

---

## Popover

**Purpose**: Rich content on click (more than tooltip).

**When to use**: Menus, forms, info panels.

**Usual contents**: Any content (forms, lists, etc.).

**Structure**:
```tsx
import {
  Popover,
  PopoverContent,
  PopoverTrigger,
} from "@/components/ui/popover"

<Popover>
  <PopoverTrigger asChild>
    <Button variant="outline">Open Popover</Button>
  </PopoverTrigger>
  <PopoverContent className="w-80">
    <div className="grid gap-4">
      <div className="space-y-2">
        <h4 className="font-medium leading-none">Dimensions</h4>
        <p className="text-sm text-muted-foreground">
          Set the dimensions for the layer.
        </p>
      </div>
      {/* More content */}
    </div>
  </PopoverContent>
</Popover>
```

**Refs**:
- shadcn Popover: https://ui.shadcn.com/docs/components/popover

---

## Progress

**Purpose**: Show completion status.

**When to use**: File uploads, multi-step processes, loading.

**Usual contents**: Progress bar, optional percentage.

**Structure**:
```tsx
import { Progress } from "@/components/ui/progress"

<Progress value={33} />
```

**With label**:
```tsx
<div className="space-y-2">
  <div className="flex justify-between text-sm">
    <span>Uploading...</span>
    <span>{progress}%</span>
  </div>
  <Progress value={progress} />
</div>
```

**Indeterminate** (no known progress):
```tsx
<Progress className="[&>div]:animate-pulse" />
```

**Accessibility**:
- `role="progressbar"` applied
- `aria-valuenow`, `aria-valuemin`, `aria-valuemax` managed

**Refs**:
- shadcn Progress: https://ui.shadcn.com/docs/components/progress

---

## Skeleton

**Purpose**: Loading placeholder that mimics content shape.

**When to use**: Initial page loads, data fetching states.

**Usual contents**: None (decorative).

**Structure**:
```tsx
import { Skeleton } from "@/components/ui/skeleton"

{/* Single skeleton */}
<Skeleton className="h-4 w-[250px]" />

{/* Card skeleton */}
<div className="flex items-center space-x-4">
  <Skeleton className="h-12 w-12 rounded-full" />
  <div className="space-y-2">
    <Skeleton className="h-4 w-[250px]" />
    <Skeleton className="h-4 w-[200px]" />
  </div>
</div>

{/* Table skeleton */}
<div className="space-y-3">
  {[...Array(5)].map((_, i) => (
    <Skeleton key={i} className="h-12 w-full" />
  ))}
</div>
```

**Pattern**: Match skeleton shape to actual content shape.

**Refs**:
- shadcn Skeleton: https://ui.shadcn.com/docs/components/skeleton

---

## Spinner

**Purpose**: Indicate loading/processing.

**When to use**: Button loading, page transitions, API calls.

**Usual contents**: Animated icon.

**Structure**:
```tsx
import { Loader2 } from "lucide-react"

{/* Simple spinner */}
<Loader2 className="h-4 w-4 animate-spin" />

{/* Centered full page */}
<div className="flex h-screen items-center justify-center">
  <Loader2 className="h-8 w-8 animate-spin text-muted-foreground" />
</div>

{/* With text */}
<div className="flex items-center gap-2">
  <Loader2 className="h-4 w-4 animate-spin" />
  <span>Loading...</span>
</div>
```

**Accessibility**:
- Add `aria-label="Loading"` or visible text
- Consider `role="status"` for live updates

## Badge / Status

**Purpose**: Small status indicator for items.

**When to use**: Status labels, counts, notifications, categories.

**Structure**:
```tsx
<span className="inline-flex items-center rounded-full border px-2.5 py-0.5 text-xs font-semibold transition-colors">
  Active
</span>
```

**Variants**:
| Variant | Classes | Use Case |
|---------|---------|----------|
| `default` | `border-transparent bg-primary text-primary-foreground` | Primary |
| `secondary` | `border-transparent bg-secondary text-secondary-foreground` | Secondary |
| `outline` | `text-foreground` | Neutral |
| `destructive` | `border-transparent bg-destructive text-destructive-foreground` | Error/Danger |
| `success` | `border-transparent bg-green-500 text-white` | Success |
| `warning` | `border-transparent bg-yellow-500 text-white` | Warning |

**With icon**:
```tsx
<Badge variant="success">
  <Check className="mr-1 h-3 w-3" />
  Verified
</Badge>
```

**Dot indicator**:
```tsx
<span className="relative flex h-3 w-3">
  <span className="animate-ping absolute inline-flex h-full w-full rounded-full bg-green-400 opacity-75"></span>
  <span className="relative inline-flex rounded-full h-3 w-3 bg-green-500"></span>
</span>
```

**Refs**:
- shadcn Badge: https://ui.shadcn.com/docs/components/badge

---

## Confetti / Celebration

**Purpose**: Visual celebration for achievements.

**When to use**: Task completion, milestones, success states.

**Structure**:
```tsx
import confetti from 'canvas-confetti'

function celebrate() {
  confetti({
    particleCount: 100,
    spread: 70,
    origin: { y: 0.6 }
  })
}

// Trigger on success
<Button onClick={() => {
  handleSuccess()
  celebrate()
}}>
  Complete
</Button>
```

**Variants**:
```tsx
// Side cannons
const defaults = { startVelocity: 30, spread: 360, ticks: 60, zIndex: 0 }

function randomInRange(min: number, max: number) {
  return Math.random() * (max - min) + min
}

confetti({
  ...defaults,
  particleCount: 50,
  origin: { x: randomInRange(0.1, 0.3), y: Math.random() - 0.2 }
})
confetti({
  ...defaults,
  particleCount: 50,
  origin: { x: randomInRange(0.7, 0.9), y: Math.random() - 0.2 }
})
```

**Accessibility**:
- Keep it optional (respect `prefers-reduced-motion`)
- Don't autoplay on load
- Provide alternative feedback

---

## Rating / Stars

**Purpose**: Display or collect rating feedback.

**When to use**: Reviews, feedback, satisfaction scores.

**Structure**:
```tsx
export function Rating({ value, max = 5, onChange, readOnly = false }: RatingProps) {
  const [hoverValue, setHoverValue] = useState<number | null>(null)
  
  return (
    <div className="flex items-center gap-1">
      {Array.from({ length: max }).map((_, i) => {
        const starValue = i + 1
        const isFilled = (hoverValue ?? value) >= starValue
        
        return (
          <button
            key={i}
            type="button"
            disabled={readOnly}
            onClick={() => onChange?.(starValue)}
            onMouseEnter={() => setHoverValue(starValue)}
            onMouseLeave={() => setHoverValue(null)}
            className={cn(
              "p-1 transition-colors",
              isFilled ? "text-yellow-400" : "text-muted-foreground",
              !readOnly && "hover:scale-110 cursor-pointer"
            )}
            aria-label={`Rate ${starValue} stars`}
          >
            <Star className="h-5 w-5" fill={isFilled ? "currentColor" : "none"} />
          </button>
        )
      })}
      
      <span className="ml-2 text-sm text-muted-foreground">
        {value} / {max}
      </span>
    </div>
  )
}
```

**Half-star precision**:
```tsx
// Use half-filled icon
<StarHalf className="h-5 w-5 text-yellow-400" fill="currentColor" />
```

**Accessibility**:
- Use proper aria-labels
- Support keyboard navigation
- Clear visual feedback

---

## Steps / Stepper

**Purpose**: Show progress through a multi-step process.

**When to use**: Onboarding, wizards, multi-step forms.

**Structure**:
```tsx
<div className="flex items-center w-full">
  {steps.map((step, index) => (
    <div key={step.id} className="flex items-center flex-1 last:flex-none">
      <div className={cn(
        "flex items-center justify-center w-8 h-8 rounded-full text-sm font-medium",
        step.isComplete && "bg-primary text-primary-foreground",
        step.isCurrent && "bg-primary/20 text-primary border-2 border-primary",
        !step.isComplete && !step.isCurrent && "bg-muted text-muted-foreground"
      )}>
        {step.isComplete ? <Check className="w-4 h-4" /> : index + 1}
      </div>
      
      <span className={cn(
        "ml-2 text-sm hidden sm:block",
        step.isCurrent ? "text-foreground font-medium" : "text-muted-foreground"
      )}>
        {step.label}
      </span>
      
      {index < steps.length - 1 && (
        <div className={cn(
          "flex-1 h-0.5 mx-4",
          step.isComplete ? "bg-primary" : "bg-muted"
        )} />
      )}
    </div>
  ))}
</div>
```

**Accessibility**:
- Use `<nav>` with aria-label
- Mark current step with `aria-current="step"`
- Show completed state clearly
