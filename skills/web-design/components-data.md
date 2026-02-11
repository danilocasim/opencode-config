---
name: components-data
description: Data display components - Table, List, Accordion, Stepper
---

# Data Display Components

Components for displaying structured data and collections.

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

## Table

**Purpose**: Display tabular data in rows and columns.

**When to use**: Data lists, admin panels, reports.

**Usual contents**: Header row, data rows, optional footer.

**Variants**:
| Variant | Description |
|---------|-------------|
| Basic | Simple header + rows |
| Striped | Alternating row backgrounds |
| Hoverable | Row highlight on hover |
| Bordered | Cell borders visible |
| Compact | Reduced padding |

**Accessibility**: Use `<thead>`, `<tbody>`, `scope="col"` on headers.

**Refs**: https://ui.shadcn.com/docs/components/table

---

## Data Table

**Purpose**: Interactive table with sorting, filtering, pagination.

**When to use**: Large datasets, admin interfaces, data management.

**Usual contents**: Toolbar (search, filters), table, pagination.

**Features**:

- Column sorting (asc/desc)
- Column visibility toggle
- Row selection (checkbox)
- Pagination controls
- Search/filter inputs
- Bulk actions

**Accessibility**: Announce sort changes, maintain focus on pagination.

**Refs**:

- https://ui.shadcn.com/docs/components/data-table
- TanStack Table: https://tanstack.com/table

---

## List

**Purpose**: Vertical collection of items.

**When to use**: Navigation, settings, feeds, search results.

**Usual contents**: List items with icon/avatar, text, optional actions.

**Variants**:
| Variant | Description |
|---------|-------------|
| Simple | Text only |
| With icon | Icon + text |
| With avatar | Avatar + text + metadata |
| With action | Trailing button/menu |
| Divided | Separator between items |
| Card | Each item in a card |

**Accessibility**: Use `<ul>`/`<ol>` semantically, `role="list"` if styled.

---

## Accordion

**Purpose**: Collapsible content sections.

**When to use**: FAQs, settings groups, dense content.

**Usual contents**: Trigger (title), collapsible panel (content).

**Variants**:
| Variant | Behavior |
|---------|----------|
| Single | Only one open at a time |
| Multiple | Multiple can be open |
| Default open | Specific items start expanded |

**Accessibility**: Arrow key navigation, Enter/Space to toggle.

**Refs**: https://ui.shadcn.com/docs/components/accordion

---

## Tree View

**Purpose**: Hierarchical data with expandable nodes.

**When to use**: File browsers, nested categories, org charts.

**Usual contents**: Parent nodes (expandable), leaf nodes, optional icons.

**Features**:

- Expand/collapse nodes
- Selection (single or multiple)
- Drag and drop (optional)
- Search/filter (optional)

**Accessibility**: `role="tree"`, `role="treeitem"`, arrow key navigation.

---

## Stepper

**Purpose**: Multi-step process indicator.

**When to use**: Wizards, checkout flows, onboarding.

**Usual contents**: Step indicators, labels, connecting lines.

**Variants**:
| Variant | Layout |
|---------|--------|
| Horizontal | Steps in a row |
| Vertical | Steps stacked |
| With icons | Icon per step |
| With description | Label + subtitle |

**States**: Completed, current, upcoming, error.

**Accessibility**: `aria-current="step"` on active step.

---

## Scroll Area

**Purpose**: Custom styled scrollable container.

**When to use**: Fixed-height containers, custom scrollbars.

**Usual contents**: Any overflowing content.

**Features**:

- Custom scrollbar styling
- Horizontal and/or vertical scroll
- Auto-hide scrollbars

**Accessibility**: Keyboard scrollable, standard scroll behavior.

**Refs**: https://ui.shadcn.com/docs/components/scroll-area

---

## Empty State

**Purpose**: Placeholder when no data exists.

**When to use**: Empty lists, no search results, first-time views.

**Usual contents**: Illustration/icon, title, description, action button.

**Variants**:
| Variant | Context |
|---------|---------|
| No data | Collection is empty |
| No results | Search/filter has no matches |
| Error | Failed to load |
| First time | User hasn't created anything yet |

**Best practices**:

- Clear explanation of why empty
- Actionable next step (CTA)
- Friendly, not blaming tone

## Kanban Board

**Purpose**: Drag-and-drop task organization in columns.

**When to use**: Project management, task tracking, workflow visualization.

**Structure**:

```tsx
<div className="flex gap-4 overflow-x-auto pb-4">
  {columns.map((column) => (
    <div key={column.id} className="w-80 flex-shrink-0">
      {/* Column header */}
      <div className="flex items-center justify-between mb-3">
        <h3 className="font-semibold">{column.title}</h3>
        <Badge variant="secondary">{column.tasks.length}</Badge>
      </div>

      {/* Tasks */}
      <div className="space-y-2 min-h-[200px] bg-muted/50 rounded-lg p-2">
        {column.tasks.map((task) => (
          <Card key={task.id} className="cursor-move">
            <CardContent className="p-3">
              <p className="font-medium text-sm">{task.title}</p>
              <div className="flex items-center gap-2 mt-2">
                <Badge variant="outline" className="text-xs">
                  {task.priority}
                </Badge>
                <span className="text-xs text-muted-foreground">{task.dueDate}</span>
              </div>
            </CardContent>
          </Card>
        ))}
      </div>

      {/* Add task button */}
      <Button variant="ghost" className="w-full mt-2" size="sm">
        <Plus className="h-4 w-4 mr-2" />
        Add Task
      </Button>
    </div>
  ))}
</div>
```

**Variants**:

```tsx
// Horizontal swimlanes
<div className="space-y-6">
  {swimlanes.map(lane => (
    <div key={lane.id}>
      <h4 className="font-medium mb-3">{lane.name}</h4>
      <div className="flex gap-4">
        {lane.columns.map(column => (...))}
      </div>
    </div>
  ))}
</div>
```

**Accessibility**:

- Keyboard navigation between columns
- ARIA live regions for updates
- Clear visual indicators for drag state

**Refs**:

- @dnd-kit: https://dndkit.com/
- react-beautiful-dnd: https://github.com/atlassian/react-beautiful-dnd

---

## Calendar / Date Picker

**Purpose**: Display and select dates.

**When to use**: Scheduling, booking, date filtering.

**Structure**:

```tsx
<Popover>
  <PopoverTrigger asChild>
    <Button variant="outline" className="w-[280px] justify-start text-left font-normal">
      <CalendarIcon className="mr-2 h-4 w-4" />
      {date ? format(date, "PPP") : <span>Pick a date</span>}
    </Button>
  </PopoverTrigger>
  <PopoverContent className="w-auto p-0">
    <Calendar mode="single" selected={date} onSelect={setDate} initialFocus />
  </PopoverContent>
</Popover>
```

**Date range picker**:

```tsx
<Calendar mode="range" selected={dateRange} onSelect={setDateRange} numberOfMonths={2} />
```

**Variants**:
| Mode | Selection | Use Case |
|------|-----------|----------|
| `single` | One date | Birthdays, deadlines |
| `range` | Start + end | Bookings, reports |
| `multiple` | Many dates | Recurring events |

**Accessibility**:

- Full keyboard navigation
- ARIA labels for dates
- Clear focus indicators

**Refs**:

- shadcn Calendar: https://ui.shadcn.com/docs/components/calendar
- react-day-picker: https://react-day-picker.js.org/

---

## Virtual List

**Purpose**: Efficiently render large lists with virtualization.

**When to use**: Lists with 1000+ items, chat messages, logs.

**Structure**:

```tsx
import { useVirtualizer } from "@tanstack/react-virtual";

function VirtualList({ items }) {
  const parentRef = useRef<HTMLDivElement>(null);

  const virtualizer = useVirtualizer({
    count: items.length,
    getScrollElement: () => parentRef.current,
    estimateSize: () => 50, // Estimated row height
  });

  return (
    <div ref={parentRef} className="h-[400px] overflow-auto">
      <div
        style={{
          height: `${virtualizer.getTotalSize()}px`,
          width: "100%",
          position: "relative",
        }}
      >
        {virtualizer.getVirtualItems().map((virtualItem) => (
          <div
            key={virtualItem.key}
            style={{
              position: "absolute",
              top: 0,
              left: 0,
              width: "100%",
              height: `${virtualItem.size}px`,
              transform: `translateY(${virtualItem.start}px)`,
            }}
          >
            {items[virtualItem.index]}
          </div>
        ))}
      </div>
    </div>
  );
}
```

**Accessibility**:

- Maintain focus when scrolling
- ARIA setsize/posinset for screen readers
- Consider pagination as alternative

**Refs**:

- @tanstack/react-virtual: https://tanstack.com/virtual/latest

---

## Filter & Search

**Purpose**: Filter and search through data sets.

**When to use**: Tables, lists, galleries with large datasets.

**Structure**:

```tsx
<div className="flex flex-col gap-4">
  {/* Search */}
  <div className="relative">
    <Search className="absolute left-3 top-1/2 -translate-y-1/2 h-4 w-4 text-muted-foreground" />
    <Input
      placeholder="Search..."
      value={searchQuery}
      onChange={(e) => setSearchQuery(e.target.value)}
      className="pl-10"
    />
  </div>

  {/* Filters */}
  <div className="flex flex-wrap gap-2">
    <Select value={status} onValueChange={setStatus}>
      <SelectTrigger className="w-[140px]">
        <SelectValue placeholder="Status" />
      </SelectTrigger>
      <SelectContent>
        <SelectItem value="all">All</SelectItem>
        <SelectItem value="active">Active</SelectItem>
        <SelectItem value="inactive">Inactive</SelectItem>
      </SelectContent>
    </Select>

    <Select value={sortBy} onValueChange={setSortBy}>
      <SelectTrigger className="w-[140px]">
        <SelectValue placeholder="Sort by" />
      </SelectTrigger>
      <SelectContent>
        <SelectItem value="name">Name</SelectItem>
        <SelectItem value="date">Date</SelectItem>
        <SelectItem value="status">Status</SelectItem>
      </SelectContent>
    </Select>

    {/* Clear filters */}
    {(searchQuery || status !== "all") && (
      <Button variant="ghost" size="sm" onClick={clearFilters}>
        <X className="h-4 w-4 mr-2" />
        Clear
      </Button>
    )}
  </div>

  {/* Active filters */}
  <div className="flex flex-wrap gap-2">
    {activeFilters.map((filter) => (
      <Badge key={filter.id} variant="secondary" className="gap-1">
        {filter.label}
        <button onClick={() => removeFilter(filter.id)}>
          <X className="h-3 w-3" />
        </button>
      </Badge>
    ))}
  </div>
</div>
```

**Accessibility**:

- Clear button labels
- ARIA live region for results count
- Keyboard shortcuts (Ctrl+K for search)
