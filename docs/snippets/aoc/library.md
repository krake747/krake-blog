---
hide:
  - toc
---

# Library

```csharp
namespace AdventOfCode.Lib;

public sealed record AocInput(
    string Text, 
    IEnumerable<string> Lines, 
    string[] AllLines
);

public static class FunctionalExtensions
{
    public static TOut Pipe<TIn, TOut>(this TIn source, Func<TIn, TOut> func) => func(source);
}
```