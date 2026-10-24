# Python

## Structure

- Use pytest.
- Use one `TestX` class for each unit under test in each file.
- Use nested classes for each method or scenario.

```python
class TestCart:
    class TestTotal:
        def test_returns_0_for_an_empty_cart(self):
            cart = Cart(PriceList())

            total = cart.total()

            assert total == 0
```

## Parameterized tests

Use `@pytest.mark.parametrize` with `ids`, or `pytest.param(..., id="...")`.

## Cleanup

Use fixtures with `yield`. Put the cleanup after `yield`. Use `tmp_path` for integration tests.

## Fakes

- Clock: inject a clock, or use `time-machine` or `freezegun`.
- File system: `pyfakefs`.

## Mutation tool

mutmut. Use `paths_to_mutate` to limit the run to the changed files.

## Coverage tool

coverage.py with `--branch`, or pytest-cov with `--cov-branch`.
