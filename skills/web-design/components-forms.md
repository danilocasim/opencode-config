---
name: components-forms
description: Form components - Input, Select, Checkbox, DatePicker, Form validation
---

# Form Components

Components for user input and data collection.

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

## Input

**Purpose**: Single-line text entry.

**When to use**: Names, emails, passwords, short text.

**Usual contents**: Label, input field, helper text, error message.

**Structure**:

```tsx
import { Input } from "@/components/ui/input";
import { Label } from "@/components/ui/label";

<div className="grid w-full max-w-sm gap-1.5">
  <Label htmlFor="email">Email</Label>
  <Input type="email" id="email" placeholder="you@example.com" />
  <p className="text-sm text-muted-foreground">We'll never share your email.</p>
</div>;
```

**Variants**:
| Variant | Use Case |
|---------|----------|
| Default | Standard text input |
| With icon | Search, URL inputs |
| With button | Search + submit |
| Error state | Validation failed |
| Disabled | Non-editable |

**With icon**:

```tsx
<div className="relative">
  <Search className="absolute left-3 top-1/2 h-4 w-4 -translate-y-1/2 text-muted-foreground" />
  <Input className="pl-10" placeholder="Search..." />
</div>
```

**Error state**:

```tsx
<div className="grid gap-1.5">
  <Label htmlFor="email">Email</Label>
  <Input id="email" className="border-destructive focus-visible:ring-destructive" />
  <p className="text-sm text-destructive">Please enter a valid email.</p>
</div>
```

**Accessibility**:

- Always associate `<Label>` with input via `htmlFor`
- Use `aria-describedby` for helper/error text
- `aria-invalid="true"` for error state

**Refs**:

- shadcn Input: https://ui.shadcn.com/docs/components/input

---

## Textarea

**Purpose**: Multi-line text entry.

**When to use**: Comments, descriptions, long-form content.

**Usual contents**: Label, textarea, character count (optional).

**Structure**:

```tsx
import { Textarea } from "@/components/ui/textarea";

<div className="grid w-full gap-1.5">
  <Label htmlFor="message">Message</Label>
  <Textarea id="message" placeholder="Type your message here." rows={4} />
</div>;
```

**Auto-resize**:

```tsx
// Using react-textarea-autosize
import TextareaAutosize from "react-textarea-autosize";

<TextareaAutosize
  className="flex min-h-[80px] w-full rounded-md border border-input bg-background px-3 py-2"
  minRows={3}
  maxRows={10}
/>;
```

**With character count**:

```tsx
const [value, setValue] = useState("")
const maxLength = 280

<div className="grid gap-1.5">
  <Textarea value={value} onChange={(e) => setValue(e.target.value)} maxLength={maxLength} />
  <p className="text-sm text-muted-foreground text-right">
    {value.length}/{maxLength}
  </p>
</div>
```

**Refs**:

- shadcn Textarea: https://ui.shadcn.com/docs/components/textarea

---

## Select

**Purpose**: Choose from a list of options.

**When to use**: Dropdowns, option selection, filters.

**Usual contents**: Trigger, options list with optional groups.

**Structure**:

```tsx
import {
  Select,
  SelectContent,
  SelectItem,
  SelectTrigger,
  SelectValue,
} from "@/components/ui/select";

<Select>
  <SelectTrigger className="w-[180px]">
    <SelectValue placeholder="Select a fruit" />
  </SelectTrigger>
  <SelectContent>
    <SelectItem value="apple">Apple</SelectItem>
    <SelectItem value="banana">Banana</SelectItem>
    <SelectItem value="orange">Orange</SelectItem>
  </SelectContent>
</Select>;
```

**With groups**:

```tsx
<SelectContent>
  <SelectGroup>
    <SelectLabel>Fruits</SelectLabel>
    <SelectItem value="apple">Apple</SelectItem>
    <SelectItem value="banana">Banana</SelectItem>
  </SelectGroup>
  <SelectSeparator />
  <SelectGroup>
    <SelectLabel>Vegetables</SelectLabel>
    <SelectItem value="carrot">Carrot</SelectItem>
  </SelectGroup>
</SelectContent>
```

**Accessibility**:

- Full keyboard support (Radix)
- `aria-expanded`, `aria-selected` managed

**Refs**:

- shadcn Select: https://ui.shadcn.com/docs/components/select

---

## Checkbox

**Purpose**: Toggle boolean value or multiple selections.

**When to use**: Agree to terms, multiple choice, feature toggles.

**Usual contents**: Checkbox, label, optional description.

**Structure**:

```tsx
import { Checkbox } from "@/components/ui/checkbox";

<div className="flex items-center space-x-2">
  <Checkbox id="terms" />
  <Label htmlFor="terms">Accept terms and conditions</Label>
</div>;
```

**With description**:

```tsx
<div className="flex items-start space-x-3">
  <Checkbox id="newsletter" className="mt-1" />
  <div className="grid gap-1.5 leading-none">
    <Label htmlFor="newsletter">Subscribe to newsletter</Label>
    <p className="text-sm text-muted-foreground">
      Receive updates about new features and releases.
    </p>
  </div>
</div>
```

**Checkbox group**:

```tsx
<div className="space-y-3">
  <Label>Select features</Label>
  {features.map((feature) => (
    <div key={feature.id} className="flex items-center space-x-2">
      <Checkbox id={feature.id} checked={selected.includes(feature.id)} />
      <Label htmlFor={feature.id}>{feature.name}</Label>
    </div>
  ))}
</div>
```

**Accessibility**:

- Use `<Label>` with `htmlFor`
- `aria-checked` managed by Radix

**Refs**:

- shadcn Checkbox: https://ui.shadcn.com/docs/components/checkbox

---

## Radio Group

**Purpose**: Select one option from a set.

**When to use**: Single selection where all options visible.

**Usual contents**: Group label, radio options with labels.

**Structure**:

```tsx
import { RadioGroup, RadioGroupItem } from "@/components/ui/radio-group";

<RadioGroup defaultValue="comfortable">
  <div className="flex items-center space-x-2">
    <RadioGroupItem value="default" id="r1" />
    <Label htmlFor="r1">Default</Label>
  </div>
  <div className="flex items-center space-x-2">
    <RadioGroupItem value="comfortable" id="r2" />
    <Label htmlFor="r2">Comfortable</Label>
  </div>
  <div className="flex items-center space-x-2">
    <RadioGroupItem value="compact" id="r3" />
    <Label htmlFor="r3">Compact</Label>
  </div>
</RadioGroup>;
```

**Card variant**:

```tsx
<RadioGroup className="grid gap-4 md:grid-cols-3">
  {plans.map((plan) => (
    <Label
      key={plan.id}
      className="flex cursor-pointer flex-col rounded-lg border p-4 hover:bg-muted [&:has(:checked)]:border-primary"
    >
      <RadioGroupItem value={plan.id} className="sr-only" />
      <span className="font-semibold">{plan.name}</span>
      <span className="text-sm text-muted-foreground">{plan.description}</span>
    </Label>
  ))}
</RadioGroup>
```

**Refs**:

- shadcn Radio Group: https://ui.shadcn.com/docs/components/radio-group

---

## Switch

**Purpose**: Toggle between two states (on/off).

**When to use**: Settings, feature toggles, preferences.

**Usual contents**: Switch, label, optional description.

**Structure**:

```tsx
import { Switch } from "@/components/ui/switch";

<div className="flex items-center space-x-2">
  <Switch id="airplane-mode" />
  <Label htmlFor="airplane-mode">Airplane Mode</Label>
</div>;
```

**Settings row pattern**:

```tsx
<div className="flex items-center justify-between">
  <div className="space-y-0.5">
    <Label htmlFor="notifications">Push notifications</Label>
    <p className="text-sm text-muted-foreground">Receive notifications on your device.</p>
  </div>
  <Switch id="notifications" />
</div>
```

**Accessibility**:

- `role="switch"` applied by Radix
- `aria-checked` managed

**Refs**:

- shadcn Switch: https://ui.shadcn.com/docs/components/switch

---

## Slider

**Purpose**: Select a value from a range.

**When to use**: Volume, price range, numeric settings.

**Usual contents**: Slider, optional value display, optional range labels.

**Structure**:

```tsx
import { Slider } from "@/components/ui/slider";

<Slider defaultValue={[50]} max={100} step={1} className="w-[60%]" />;
```

**With value display**:

```tsx
const [value, setValue] = useState([50])

<div className="space-y-4">
  <div className="flex justify-between">
    <Label>Volume</Label>
    <span className="text-sm text-muted-foreground">{value}%</span>
  </div>
  <Slider value={value} onValueChange={setValue} max={100} step={1} />
</div>
```

**Range slider**:

```tsx
<Slider defaultValue={[25, 75]} max={100} step={1} />
```

**Refs**:

- shadcn Slider: https://ui.shadcn.com/docs/components/slider

---

## Date Picker

**Purpose**: Select a date or date range.

**When to use**: Booking, scheduling, filtering by date.

**Usual contents**: Input trigger, calendar popover.

**Structure**:

```tsx
import { Calendar } from "@/components/ui/calendar"
import { Popover, PopoverContent, PopoverTrigger } from "@/components/ui/popover"
import { format } from "date-fns"

const [date, setDate] = useState<Date>()

<Popover>
  <PopoverTrigger asChild>
    <Button variant="outline" className={cn("w-[280px] justify-start text-left font-normal", !date && "text-muted-foreground")}>
      <CalendarIcon className="mr-2 h-4 w-4" />
      {date ? format(date, "PPP") : <span>Pick a date</span>}
    </Button>
  </PopoverTrigger>
  <PopoverContent className="w-auto p-0">
    <Calendar mode="single" selected={date} onSelect={setDate} initialFocus />
  </PopoverContent>
</Popover>
```

**Date range**:

```tsx
<Calendar mode="range" selected={dateRange} onSelect={setDateRange} numberOfMonths={2} />
```

**Accessibility**:

- Full keyboard navigation
- `aria-label` for calendar

**Refs**:

- shadcn Calendar: https://ui.shadcn.com/docs/components/calendar
- shadcn Date Picker: https://ui.shadcn.com/docs/components/date-picker

---

## File Upload

**Purpose**: Upload files from device.

**When to use**: Document uploads, image uploads, attachments.

**Usual contents**: Drop zone, file input, preview, progress.

**Structure**:

```tsx
{
  /* Simple file input */
}
<div className="grid w-full max-w-sm gap-1.5">
  <Label htmlFor="file">Upload file</Label>
  <Input id="file" type="file" />
</div>;

{
  /* Drop zone */
}
<div className="flex flex-col items-center justify-center rounded-lg border border-dashed p-12">
  <Upload className="h-8 w-8 text-muted-foreground" />
  <p className="mt-2 text-sm text-muted-foreground">
    Drag and drop or{" "}
    <label className="cursor-pointer text-primary hover:underline">
      browse
      <input type="file" className="sr-only" />
    </label>
  </p>
  <p className="mt-1 text-xs text-muted-foreground">PNG, JPG up to 10MB</p>
</div>;
```

**With preview**:

```tsx
{
  file && (
    <div className="flex items-center gap-4 rounded-lg border p-4">
      <FileIcon className="h-8 w-8 text-muted-foreground" />
      <div className="flex-1 min-w-0">
        <p className="truncate font-medium">{file.name}</p>
        <p className="text-sm text-muted-foreground">{formatBytes(file.size)}</p>
      </div>
      <Button variant="ghost" size="icon" onClick={removeFile}>
        <X className="h-4 w-4" />
      </Button>
    </div>
  );
}
```

**Accessibility**:

- Label the file input
- Announce upload status

---

## Combobox (Autocomplete)

**Purpose**: Searchable select with filtering.

**When to use**: Large option lists, country selectors, tag inputs.

**Usual contents**: Search input, filtered options list.

**Structure**:

```tsx
import { Command, CommandEmpty, CommandGroup, CommandInput, CommandItem } from "@/components/ui/command"
import { Popover, PopoverContent, PopoverTrigger } from "@/components/ui/popover"

const [open, setOpen] = useState(false)
const [value, setValue] = useState("")

<Popover open={open} onOpenChange={setOpen}>
  <PopoverTrigger asChild>
    <Button variant="outline" role="combobox" aria-expanded={open} className="w-[200px] justify-between">
      {value ? options.find((o) => o.value === value)?.label : "Select option..."}
      <ChevronsUpDown className="ml-2 h-4 w-4 shrink-0 opacity-50" />
    </Button>
  </PopoverTrigger>
  <PopoverContent className="w-[200px] p-0">
    <Command>
      <CommandInput placeholder="Search..." />
      <CommandEmpty>No results found.</CommandEmpty>
      <CommandGroup>
        {options.map((option) => (
          <CommandItem key={option.value} value={option.value} onSelect={(v) => { setValue(v); setOpen(false) }}>
            <Check className={cn("mr-2 h-4 w-4", value === option.value ? "opacity-100" : "opacity-0")} />
            {option.label}
          </CommandItem>
        ))}
      </CommandGroup>
    </Command>
  </PopoverContent>
</Popover>
```

**Refs**:

- shadcn Combobox: https://ui.shadcn.com/docs/components/combobox

---

## Search

**Purpose**: Search input with optional suggestions.

**When to use**: Site search, filtering, command palettes.

**Usual contents**: Search icon, input, clear button, suggestions.

**Structure**:

```tsx
<div className="relative">
  <Search className="absolute left-3 top-1/2 h-4 w-4 -translate-y-1/2 text-muted-foreground" />
  <Input
    placeholder="Search..."
    className="pl-10 pr-10"
    value={query}
    onChange={(e) => setQuery(e.target.value)}
  />
  {query && (
    <Button
      variant="ghost"
      size="icon"
      className="absolute right-1 top-1/2 -translate-y-1/2 h-7 w-7"
      onClick={() => setQuery("")}
    >
      <X className="h-4 w-4" />
    </Button>
  )}
</div>
```

**With keyboard shortcut hint**:

```tsx
<div className="relative">
  <Search className="absolute left-3 top-1/2 h-4 w-4 -translate-y-1/2 text-muted-foreground" />
  <Input placeholder="Search..." className="pl-10 pr-16" />
  <kbd className="absolute right-3 top-1/2 -translate-y-1/2 pointer-events-none inline-flex h-5 select-none items-center gap-1 rounded border bg-muted px-1.5 font-mono text-[10px] font-medium text-muted-foreground">
    <span className="text-xs">⌘</span>K
  </kbd>
</div>
```

---

## Form (with Validation)

**Purpose**: Complete form with validation and submission.

**When to use**: Any multi-field form.

**Usual contents**: Multiple fields, validation messages, submit button.

**Structure** (with React Hook Form + Zod):

```tsx
import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import * as z from "zod";
import {
  Form,
  FormControl,
  FormDescription,
  FormField,
  FormItem,
  FormLabel,
  FormMessage,
} from "@/components/ui/form";

const formSchema = z.object({
  email: z.string().email("Invalid email address"),
  password: z.string().min(8, "Password must be at least 8 characters"),
});

function MyForm() {
  const form = useForm<z.infer<typeof formSchema>>({
    resolver: zodResolver(formSchema),
    defaultValues: { email: "", password: "" },
  });

  function onSubmit(values: z.infer<typeof formSchema>) {
    console.log(values);
  }

  return (
    <Form {...form}>
      <form onSubmit={form.handleSubmit(onSubmit)} className="space-y-6">
        <FormField
          control={form.control}
          name="email"
          render={({ field }) => (
            <FormItem>
              <FormLabel>Email</FormLabel>
              <FormControl>
                <Input placeholder="you@example.com" {...field} />
              </FormControl>
              <FormDescription>Your email address.</FormDescription>
              <FormMessage />
            </FormItem>
          )}
        />
        <FormField
          control={form.control}
          name="password"
          render={({ field }) => (
            <FormItem>
              <FormLabel>Password</FormLabel>
              <FormControl>
                <Input type="password" {...field} />
              </FormControl>
              <FormMessage />
            </FormItem>
          )}
        />
        <Button type="submit">Submit</Button>
      </form>
    </Form>
  );
}
```

**Refs**:

- shadcn Form: https://ui.shadcn.com/docs/components/form
- React Hook Form: https://react-hook-form.com/
- Zod: https://zod.dev/

## Multi-Step Wizard

**Purpose**: Break long forms into manageable steps.

**When to use**: Checkout flows, onboarding, complex configurations, surveys.

**Structure**:

```tsx
export function WizardForm() {
  const [step, setStep] = useState(1);
  const [data, setData] = useState({});
  const totalSteps = 3;

  const updateData = (stepData: any) => {
    setData((prev) => ({ ...prev, ...stepData }));
  };

  const next = () => setStep((s) => Math.min(s + 1, totalSteps));
  const back = () => setStep((s) => Math.max(s - 1, 1));

  return (
    <div className="max-w-2xl mx-auto">
      {/* Progress indicator */}
      <div className="mb-8">
        <div className="flex justify-between mb-2">
          {Array.from({ length: totalSteps }).map((_, i) => (
            <div
              key={i}
              className={cn(
                "flex items-center justify-center w-8 h-8 rounded-full text-sm font-medium",
                step > i + 1 && "bg-primary text-primary-foreground",
                step === i + 1 && "bg-primary/20 text-primary border-2 border-primary",
                step < i + 1 && "bg-muted text-muted-foreground"
              )}
            >
              {step > i + 1 ? <Check className="w-4 h-4" /> : i + 1}
            </div>
          ))}
        </div>
        <Progress value={(step / totalSteps) * 100} />
      </div>

      {/* Step content */}
      <div className="border rounded-lg p-6">
        {step === 1 && <StepOne data={data} onNext={next} updateData={updateData} />}
        {step === 2 && <StepTwo data={data} onNext={next} onBack={back} updateData={updateData} />}
        {step === 3 && <StepThree data={data} onBack={back} onSubmit={handleSubmit} />}
      </div>

      {/* Step indicator text */}
      <p className="text-center text-sm text-muted-foreground mt-4">
        Step {step} of {totalSteps}
      </p>
    </div>
  );
}
```

**Individual step component**:

```tsx
function StepOne({ data, onNext, updateData }: StepProps) {
  const form = useForm({
    resolver: zodResolver(stepOneSchema),
    defaultValues: data,
  });

  const onSubmit = (values: any) => {
    updateData(values);
    onNext();
  };

  return (
    <Form {...form}>
      <form onSubmit={form.handleSubmit(onSubmit)} className="space-y-4">
        <h2 className="text-lg font-semibold">Personal Information</h2>

        <FormField
          control={form.control}
          name="name"
          render={({ field }) => (
            <FormItem>
              <FormLabel>Full Name</FormLabel>
              <FormControl>
                <Input {...field} />
              </FormControl>
              <FormMessage />
            </FormItem>
          )}
        />

        <div className="flex justify-end">
          <Button type="submit">
            Continue
            <ArrowRight className="ml-2 h-4 w-4" />
          </Button>
        </div>
      </form>
    </Form>
  );
}
```

**Review step**:

```tsx
function ReviewStep({ data, onBack, onSubmit }: ReviewProps) {
  return (
    <div className="space-y-6">
      <h2 className="text-lg font-semibold">Review Your Information</h2>

      <dl className="space-y-4">
        <div className="flex justify-between py-2 border-b">
          <dt className="text-muted-foreground">Name</dt>
          <dd className="font-medium">{data.name}</dd>
        </div>
        <div className="flex justify-between py-2 border-b">
          <dt className="text-muted-foreground">Email</dt>
          <dd className="font-medium">{data.email}</dd>
        </div>
      </dl>

      <div className="flex justify-between">
        <Button variant="outline" onClick={onBack}>
          <ArrowLeft className="mr-2 h-4 w-4" />
          Back
        </Button>
        <Button onClick={onSubmit}>Submit</Button>
      </div>
    </div>
  );
}
```

**Accessibility**:

- Announce step changes to screen readers
- Maintain focus management between steps
- Allow navigation back to previous steps
- Show overall progress

---

## Inline Edit

**Purpose**: Edit data in-place without navigating to a separate page.

**When to use**: Quick edits, tables, profile information, settings.

**Structure**:

```tsx
export function InlineEdit({ value, onSave, label }: InlineEditProps) {
  const [isEditing, setIsEditing] = useState(false);
  const [editValue, setEditValue] = useState(value);
  const inputRef = useRef<HTMLInputElement>(null);

  useEffect(() => {
    if (isEditing) {
      inputRef.current?.focus();
      inputRef.current?.select();
    }
  }, [isEditing]);

  const handleSave = () => {
    onSave(editValue);
    setIsEditing(false);
  };

  const handleCancel = () => {
    setEditValue(value);
    setIsEditing(false);
  };

  const handleKeyDown = (e: React.KeyboardEvent) => {
    if (e.key === "Enter") handleSave();
    if (e.key === "Escape") handleCancel();
  };

  if (isEditing) {
    return (
      <div className="flex items-center gap-2">
        <Input
          ref={inputRef}
          value={editValue}
          onChange={(e) => setEditValue(e.target.value)}
          onKeyDown={handleKeyDown}
          className="h-8"
          aria-label={`Edit ${label}`}
        />
        <Button size="sm" variant="ghost" onClick={handleSave}>
          <Check className="h-4 w-4" />
        </Button>
        <Button size="sm" variant="ghost" onClick={handleCancel}>
          <X className="h-4 w-4" />
        </Button>
      </div>
    );
  }

  return (
    <button
      onClick={() => setIsEditing(true)}
      className="flex items-center gap-2 group"
      aria-label={`Edit ${label}`}
    >
      <span>{value}</span>
      <Pencil className="h-3 w-3 opacity-0 group-hover:opacity-50" />
    </button>
  );
}
```

**Table cell inline edit**:

```tsx
function EditableCell({ value, onSave }: CellProps) {
  const [isEditing, setIsEditing] = useState(false);

  return (
    <TableCell>
      {isEditing ? (
        <Input
          defaultValue={value}
          onBlur={(e) => {
            onSave(e.target.value);
            setIsEditing(false);
          }}
          onKeyDown={(e) => {
            if (e.key === "Enter") {
              onSave(e.currentTarget.value);
              setIsEditing(false);
            }
          }}
          className="h-8"
          autoFocus
        />
      ) : (
        <span
          onClick={() => setIsEditing(true)}
          className="cursor-pointer hover:bg-muted px-2 py-1 rounded -mx-2"
        >
          {value}
        </span>
      )}
    </TableCell>
  );
}
```

**Inline form (edit multiple fields)**:

```tsx
export function InlineProfileEdit() {
  const [isEditing, setIsEditing] = useState(false);
  const form = useForm({ defaultValues: user });

  const onSubmit = (data: any) => {
    updateUser(data);
    setIsEditing(false);
  };

  return (
    <Card>
      <CardHeader className="flex flex-row items-center justify-between">
        <CardTitle>Profile</CardTitle>
        {!isEditing && (
          <Button variant="ghost" size="sm" onClick={() => setIsEditing(true)}>
            <Pencil className="h-4 w-4 mr-2" />
            Edit
          </Button>
        )}
      </CardHeader>
      <CardContent>
        {isEditing ? (
          <Form {...form}>
            <form onSubmit={form.handleSubmit(onSubmit)} className="space-y-4">
              <FormField
                control={form.control}
                name="name"
                render={({ field }) => (
                  <FormItem>
                    <FormLabel>Name</FormLabel>
                    <FormControl>
                      <Input {...field} />
                    </FormControl>
                  </FormItem>
                )}
              />

              <div className="flex gap-2">
                <Button type="submit">Save</Button>
                <Button type="button" variant="outline" onClick={() => setIsEditing(false)}>
                  Cancel
                </Button>
              </div>
            </form>
          </Form>
        ) : (
          <dl className="space-y-2">
            <div>
              <dt className="text-sm text-muted-foreground">Name</dt>
              <dd className="font-medium">{user.name}</dd>
            </div>
            <div>
              <dt className="text-sm text-muted-foreground">Email</dt>
              <dd className="font-medium">{user.email}</dd>
            </div>
          </dl>
        )}
      </CardContent>
    </Card>
  );
}
```

**Accessibility**:

- Clear edit/save/cancel actions
- Keyboard support (Enter to save, Escape to cancel)
- Focus management on edit
- Visual feedback for editable fields

---

## Form Layout Patterns

### Two-Column Layout

```tsx
<div className="grid grid-cols-1 md:grid-cols-2 gap-4">
  <FormField name="firstName" ... />
  <FormField name="lastName" ... />
  <FormField name="email" className="md:col-span-2" ... />
  <FormField name="city" ... />
  <FormField name="zip" ... />
</div>
```

### Fieldsets with Legend

```tsx
<fieldset className="border rounded-lg p-4 space-y-4">
  <legend className="text-sm font-medium px-2">Address</legend>
  <FormField name="street" ... />
  <FormField name="city" ... />
</fieldset>
```

### Sticky Actions

```tsx
<div className="relative">
  <div className="space-y-4 pb-20">{/* Form fields */}</div>

  <div className="fixed bottom-0 left-0 right-0 border-t bg-background p-4">
    <div className="container flex justify-end gap-2">
      <Button variant="outline">Cancel</Button>
      <Button type="submit">Save Changes</Button>
    </div>
  </div>
</div>
```

**Accessibility**:

- Group related fields with `<fieldset>`
- Use `<legend>` for group labels
- Maintain logical tab order
- Show validation errors inline
