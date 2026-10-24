# Kotlin

## Structure

If the repository uses Kotest, use `DescribeSpec`. Use one root `describe` for each file and nested `describe` blocks.

Otherwise, use JUnit 5:

- Use one test class for each unit under test.
- Use `@Nested inner class` for each method or scenario.
- Use backtick names.

```kotlin
class CartTest {

    @Nested
    inner class Total {

        @Test
        fun `returns 0 for an empty cart`() {
            val cart = Cart(PriceList())

            val total = cart.total()

            assertThat(total).isZero()
        }
    }
}
```

## Parameterized tests

JUnit 5: `@ParameterizedTest(name = "{0}")`. Kotest: `withData`.

## Cleanup

JUnit 5: `@BeforeEach`, `@AfterEach`, and `@AfterAll`. Kotest: `beforeEach`, `afterEach`, and `afterSpec`.

## Fakes

- Clock: inject `java.time.Clock` or `kotlinx.datetime.Clock`.
- File system: Jimfs or Okio `FakeFileSystem`.

## Mutation tool

PIT (`pitest`) with the Kotlin plugin.

## Coverage tool

Kover or JaCoCo. Read the branch counters of the report.
