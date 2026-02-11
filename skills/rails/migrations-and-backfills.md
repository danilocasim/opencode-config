# Migrations and Backfills

Production migrations must be safe: avoid long locks, avoid table rewrites, and separate schema changes from data backfills.

## When to load

- You are adding a migration on a table with real traffic.
- You need a backfill plan (batching, resumability).
- You need a zero-downtime sequence (expand -> backfill -> contract).

## When NOT to load

- You are writing domain code unrelated to schema changes.
- You are fixing a failing query/index without migrations (use DB skill).

## Core rules

- Prefer expand/contract: add new columns first, deploy, backfill, then switch reads/writes.
- Keep migrations fast and reversible; avoid loading application models.
- Backfills should be resumable and rate-limited (batch + sleep if needed).
- Avoid `change_column` type changes that rewrite whole tables.
- Add indexes concurrently when supported.

## Minimal examples

Expand: add nullable column (fast):

```ruby
class AddNormalizedEmailToUsers < ActiveRecord::Migration[7.1]
  def change
    add_column :users, :normalized_email, :string
    add_index :users, :normalized_email
  end
end
```

Backfill as a job (resumable batches):

```ruby
class BackfillNormalizedEmailJob < ApplicationJob
  def perform(last_id: 0)
    scope = User.where("id > ?", last_id).order(:id).limit(1_000)
    ids = scope.pluck(:id)
    return if ids.empty?

    User.where(id: ids).find_each do |u|
      u.update_columns(normalized_email: u.email.to_s.strip.downcase)
    end

    self.class.perform_later(last_id: ids.last)
  end
end
```

Contract (later deploy): make it required once fully backfilled.

## Anti-patterns

- Data backfills inside a migration that runs during deploy.
- Iterating with `User.all.each` (loads too much, no batching).
- Using application models with validations/callbacks in backfills.
- Non-idempotent backfills that cannot be re-run safely.

## Checklist

- Is this an expand/contract sequence?
- Is the backfill resumable and bounded?
- Are you avoiding model callbacks/validations in bulk updates?
- Are you avoiding long-running locks/table rewrites?
- Do you have a rollback plan?
