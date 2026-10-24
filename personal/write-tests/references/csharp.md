# C#

## Structure

- Use one test class for each unit under test.
- Use nested classes for each method or scenario.
- Use the framework of the repository: xUnit, NUnit, or MSTest.

```csharp
public class CartTests
{
    public class Total
    {
        [Fact]
        public void Returns_0_for_an_empty_cart()
        {
            var cart = new Cart(new PriceList());

            var total = cart.Total();

            Assert.Equal(0, total);
        }
    }
}
```

## Parameterized tests

xUnit: `[Theory]` with `[InlineData]` or `[MemberData]`. NUnit: `[TestCase(..., TestName = "...")]`.

## Cleanup

xUnit: constructor and `IDisposable` or `IAsyncLifetime`. NUnit: `[SetUp]`, `[TearDown]`, and `[OneTimeTearDown]`.

## Fakes

- Clock: inject `TimeProvider`. Use `FakeTimeProvider` in tests.
- File system: `System.IO.Abstractions` with `MockFileSystem`.

## Mutation tool

Stryker.NET (`dotnet stryker`). Use `--mutate` to limit the run to the changed files.

## Coverage tool

coverlet (`dotnet test --collect:"XPlat Code Coverage"`). Read the branch rate of the report.
