---
name: rails
description: Ruby on Rails conventions (Rails 7.x/8.x, 2024-2026)
---

# Rails Conventions (Rails 7.x/8.x)

## Core Principles
- **Convention over Configuration**
- **DRY** - Don't Repeat Yourself
- **Fat models, skinny controllers**

## Modern Rails (7.x/8.x)
- **Hotwire**: Turbo + Stimulus over heavy JS
- **Import maps**: Default for JS (no bundler needed)
- **Propshaft**: Asset pipeline replacement
- **Solid Queue/Cache/Cable**: Database-backed adapters

## File Structure
```
app/
  models/          # Business logic
  controllers/     # Request handling
  views/           # Templates
  helpers/         # View helpers
  jobs/            # Background jobs
  mailers/         # Email
  components/      # ViewComponents (recommended)
config/
db/
  migrate/         # Migrations
test/ or spec/
```

## Models
- One model per file
- Validations at the top
- Associations after validations
- Scopes for common queries
- Callbacks sparingly (prefer service objects)

```ruby
class User < ApplicationRecord
  # Constants
  ROLES = %w[admin member guest].freeze

  # Associations
  has_many :posts, dependent: :destroy
  belongs_to :organization

  # Validations
  validates :email, presence: true, uniqueness: true
  validates :role, inclusion: { in: ROLES }

  # Scopes
  scope :active, -> { where(active: true) }
  scope :admins, -> { where(role: 'admin') }

  # Instance methods
  def full_name
    "#{first_name} #{last_name}"
  end
end
```

## Controllers
- 7 RESTful actions max
- Use `before_action` for shared logic
- Strong parameters for mass assignment
- Respond to multiple formats when needed

## Service Objects
- For complex business logic
- Single responsibility
- `call` as the public interface

```ruby
class Users::Create
  def initialize(params)
    @params = params
  end

  def call
    User.create!(@params)
  end
end
```

## Testing
- RSpec or Minitest
- FactoryBot for fixtures
- System tests with Capybara
- Request specs over controller specs

## Tools
- Rubocop + rubocop-rails
- Brakeman for security
- bullet for N+1 queries

## Reference Docs
- Rails Guides: https://guides.rubyonrails.org/
- Rails API: https://api.rubyonrails.org/
- Rails Style Guide: https://rails.rubystyle.guide/

