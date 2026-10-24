# Rust

## Structure

- Use one `#[cfg(test)] mod tests` for each file.
- Use nested modules for each function or scenario.

```rust
#[cfg(test)]
mod tests {
    use super::*;

    mod total {
        use super::*;

        #[test]
        fn returns_0_for_an_empty_cart() {
            let cart = Cart::new(PriceList::new());

            let total = cart.total();

            assert_eq!(total, 0);
        }
    }
}
```

## Parameterized tests

Use `rstest` with `#[case::name(...)]`, if the repository uses it.

## Cleanup

Use a guard type that cleans up in `Drop`. Use `tempfile::TempDir` for integration tests.

## Fakes

- Clock: inject a clock trait or a `fn() -> SystemTime`.
- File system: inject a trait. Use an in-memory implementation in tests.

## Mutation tool

cargo-mutants. Use `--file` or `--in-diff` to limit the run to the changed code.

## Coverage tool

cargo-llvm-cov with `--branch`. Branch coverage needs a nightly toolchain. On a stable toolchain, use the manual branch list from the skill.
