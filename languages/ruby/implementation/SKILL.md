---
name: ruby-implementation
description: Ruby/Rails pitfalls — N+1 queries, callback hell, mass assignment. Load when writing or reviewing .rb files.
---

# Ruby/Rails Implementation — What Claude Gets Wrong

## ActiveRecord Pitfalls
- **N+1 queries** — Claude's most frequent Rails mistake. Use `includes()`, `preload()`, or `eager_load()`
- `find` raises `ActiveRecord::RecordNotFound`, `find_by` returns `nil` — choose consciously
- **Strong parameters**: `params.require(:user).permit(:name, :email)` — never `params.permit!`
- `update` vs `update!`: bang version raises on validation failure — use `!` when failure is unexpected
- Scopes over class methods for chainable queries

## Rails Conventions Claude Breaks
- **Fat models, skinny controllers** — but don't dump everything in models either. Use service objects.
- Callbacks (`before_save`, `after_create`) are dangerous — they hide side effects. Prefer explicit service objects.
- `has_many :through` over `has_and_belongs_to_many` — join model gives you flexibility
- Migrations: never modify old migrations — create new ones

## Ruby Patterns
- `freeze` string literals: `# frozen_string_literal: true` at file top
- `&.` safe navigation over `try()` — more idiomatic, nil-safe
- Symbol over string for hash keys: `{ name: "Alice" }` not `{ "name" => "Alice" }`
- `Struct` or `Data` (Ruby 3.2+) for simple value objects — not full classes

## Common Bugs
- **`==` vs `eql?` vs `equal?`**: `==` for value, `equal?` for identity — Claude sometimes confuses
- Mutable default arguments: `def foo(arr = [])` creates ONE shared array — use `nil` + `||=`
- `return` in blocks: use `next` to skip, not `return` (which exits the method)

## Build Verification
- `bundle exec rails db:migrate` → `bundle exec rubocop` → `bundle exec rspec` or `rails test`
