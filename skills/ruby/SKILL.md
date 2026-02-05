---
name: ruby
description: Ruby 3.x conventions, idioms, and best practices (2024-2026)
---

# Ruby Conventions (Ruby 3.x)

## Style Essentials
- 2 spaces indentation, no tabs
- Max 80 chars per line (120 acceptable for modern displays)
- UTF-8 encoding
- Unix line endings
- Trailing newline at EOF

## Naming
- `snake_case`: methods, variables, symbols, files, directories
- `CamelCase`: classes, modules
- `SCREAMING_SNAKE_CASE`: constants
- `predicate?`: methods returning boolean
- `dangerous!`: methods modifying self (only if safe version exists)
- Prefix unused vars with `_`

## Modern Ruby (3.x)
- **Pattern matching**: Use `case/in` for complex conditionals
- **Endless methods**: `def square(x) = x * x` for one-liners
- **Numbered block params**: `[1,2,3].map { _1 * 2 }` (use sparingly)
- **Hash shorthand**: `{x:, y:}` instead of `{x: x, y: y}`
- **Data class**: `Data.define(:x, :y)` for immutable value objects
- **Keyword args**: Prefer over positional for 3+ params

## Control Flow
- `&&`/`||` for boolean, `and`/`or` for control flow only
- `unless` for negative conditions (no `else` with `unless`)
- Ternary for simple conditionals only
- `case/when` over long `if/elsif` chains
- Avoid `for` loops, use iterators

## Blocks
- `{ }` for single-line, `do/end` for multi-line
- Use `&:method` shorthand: `names.map(&:upcase)`

## Classes
- Composition over inheritance
- `attr_reader`/`attr_accessor` over manual getters/setters
- Group: constants, attr_*, class methods, initialize, public, protected, private
- Use `Struct.new` or `Data.define` for simple data containers

## Error Handling
- `raise` over `fail`
- Specific exceptions over generic `StandardError`
- `raise ... from` for exception chaining (Ruby 3.2+)

## Testing
- RSpec preferred, Minitest acceptable
- One assertion per test (usually)
- Descriptive `it` blocks: `it "returns nil when user not found"`

## Documentation (YARD)

Use YARD for public APIs.

```ruby
# Calculates the total price including discounts and tax.
#
# Why: The UI needs a single canonical price calculation to avoid drift between
# checkout, invoices, and email receipts.
#
# @param items [Array<CartItem>]
# @param shipping_address [Address]
# @return [Money]
# @raise [InvalidAddressError] If address is incomplete
def calculate_total(items, shipping_address)
  # ...
end
```

Guidelines:
- Prefer `@param`, `@return`, `@raise`, `@example`.
- Document side effects (DB writes, network calls) explicitly.

## Tools
- **Rubocop**: Linting and formatting
- **Sorbet/RBS**: Type checking (optional but recommended)

## Reference Docs
- Style Guide: https://rubystyle.guide/
- RuboCop: https://docs.rubocop.org/
- Ruby 3.x News: https://www.ruby-lang.org/en/news/
