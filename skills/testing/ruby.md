# Ruby/Rails Testing (RSpec/Minitest)

## Defaults

- Prefer RSpec when present
- Use factories (FactoryBot) where the project already uses them
- Prefer request/system specs for Rails behavior

## RSpec examples

```ruby
RSpec.describe NormalizeEmail do
  it "downcases and trims" do
    expect(described_class.call("  A@B.COM ")).to eq("a@b.com")
  end
end
```

## Error paths

```ruby
it "raises on invalid email" do
  expect { described_class.call("nope") }.to raise_error(ArgumentError)
end
```

## Rails requests

- Prefer request specs over controller specs
- Assert status + key JSON fields
