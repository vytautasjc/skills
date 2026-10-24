# Ruby

## Structure

- Use RSpec.
- Use one root `describe` for each file. Name it after the class under test.
- Use nested `describe` blocks for each method, e.g. `describe "#total"`.
- Use `context` for scenarios.

```ruby
RSpec.describe Cart do
  describe "#total" do
    it "returns 0 for an empty cart" do
      cart = Cart.new(PriceList.new)

      total = cart.total

      expect(total).to eq(0)
    end
  end
end
```

## Parameterized tests

Use a `context` for each case. Do not use loops to generate tests.

## Cleanup

Use `before`, `after`, and `around` hooks. Use `Dir.mktmpdir` with a block for integration tests.

## Fakes

- Clock: inject a clock, or use `ActiveSupport::Testing::TimeHelpers`.
- File system: `fakefs`.

## Mutation tool

mutant. Use `--since` to limit the run to the changed code.

## Coverage tool

SimpleCov with `enable_coverage :branch`.
