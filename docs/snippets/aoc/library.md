---
hide:
  - toc
---

# Library

```csharp
namespace AdventOfCode.Lib;

public sealed class AocInput
{
    public required string Text { get; init; }
    public required IEnumerable<string> Lines { get; init; }
    public required string[] AllLines { get; init; }
}

public static class FunctionalExtensions
{
    public static TOut Pipe<TIn, TOut>(this TIn source, Func<TIn, TOut> func) => func(source);
}
```