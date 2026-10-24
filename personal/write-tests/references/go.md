# Go

## Structure

- Use one `TestX` function for each unit under test.
- Use `t.Run` subtests for each method or scenario. Nest `t.Run` calls to make groups.

```go
func TestCart(t *testing.T) {
	t.Run("Total", func(t *testing.T) {
		t.Run("returns 0 for an empty cart", func(t *testing.T) {
			cart := NewCart(NewPriceList())

			total := cart.Total()

			if total != 0 {
				t.Fatalf("got %d, want 0", total)
			}
		})
	})
}
```

The comparison in the Assert section is the assertion. It is not test logic.

## Parameterized tests

Use table-driven tests with a `name` field. Run each case in `t.Run(tc.name, ...)`.

## Cleanup

Use `t.Cleanup`. Use `t.TempDir()` for integration tests.

## Fakes

- Clock: inject a `func() time.Time` or a clock interface.
- File system: accept an `fs.FS`. Use `testing/fstest.MapFS` in tests.

## Mutation tool

Gremlins (`go-gremlins/gremlins`).

## Coverage tool

`go test -cover` reports statement coverage only. Use the manual branch list from the skill.
