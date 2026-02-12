---
name: ruby-testing
description: Ruby/Rails test pitfalls — RSpec let vs let!, factory vs fixture, controller vs request specs. Load only when writing or reviewing *_spec.rb or *_test.rb files.
---

# Ruby/Rails Testing — What Claude Gets Wrong

## RSpec vs Minitest
- **Check the project first** — Rails defaults to Minitest, but many projects use RSpec
- Don't mix frameworks in the same project

## RSpec Pitfalls
- **`let` is lazy, `let!` is eager** — Claude often uses `let` when side effects are needed at setup time
- `subject` for the thing under test — but explicit is better than magic
- `described_class` over hardcoding class names
- `context` for conditions ("when logged in"), `describe` for units ("#create")
- **Don't use `before(:all)`** — state leaks between tests. Use `before(:each)` (default)

## Factory vs Fixture
- **FactoryBot**: `create` hits DB, `build` doesn't, `build_stubbed` fakes persistence — Claude defaults to `create` when `build` suffices
- Traits for variations: `create(:user, :admin)` not separate factories
- Avoid deeply nested factories — they slow tests and obscure intent
- **Fixtures** (Minitest default): faster but less flexible. Don't mix with FactoryBot.

## Controller vs Request Specs
- **Request specs over controller specs** — controller specs are deprecated in modern RSpec Rails
- `get`, `post`, `patch`, `delete` with path, not controller action
- Test HTTP status, JSON body, redirects — not instance variables

## Common Mistakes
- **`expect { ... }.to change { ... }.by(1)`** — the block form. Claude sometimes writes `expect(thing).to change(...)` which doesn't work
- `allow` for stubs, `expect().to receive` for mocks — don't mix their intent
- `have_http_status(:ok)` over `have_http_status(200)` — more readable
- Database cleaner: `transaction` strategy for unit, `truncation` for feature/system tests

## Build Verification
- `bundle exec rspec` or `rails test` → `bundle exec rubocop`
