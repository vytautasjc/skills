# Java

## Structure

- Use one test class for each unit under test.
- Use JUnit 5 `@Nested` classes for each method or scenario.
- Use `@DisplayName` for readable names.

```java
@DisplayName("Cart")
class CartTest {

    @Nested
    @DisplayName("total")
    class Total {

        @Test
        @DisplayName("returns 0 for an empty cart")
        void returnsZeroForEmptyCart() {
            var cart = new Cart(new PriceList());

            var total = cart.total();

            assertThat(total).isZero();
        }
    }
}
```

## Parameterized tests

Use `@ParameterizedTest` with `name = "{0}"`, and `@MethodSource` or `@CsvSource`.

## Cleanup

Use `@BeforeEach`, `@AfterEach`, and `@AfterAll`. Use `@TempDir` for integration tests.

## Fakes

- Clock: inject `java.time.Clock`. Use `Clock.fixed(...)` in tests.
- File system: Jimfs.

## Mutation tool

PIT (`pitest`). Use `targetClasses` to limit the run to the changed classes.

## Coverage tool

JaCoCo. Read the branch counters of the report.
