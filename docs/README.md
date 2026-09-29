# Patterns notebook

Short reminders for C# and TypeScript. Open a page when you need a nudge — a syntax form, a common pattern, or a gotcha. These are notes, not tutorials.

<div class="lang-switch">
  <a class="lang-card lang-cs" href="#/csharp/">
    <span class="lang-kicker">C#</span>
    <strong>Syntax, nulls, LINQ, async</strong>
    <span>Records, collections, lambdas</span>
  </a>
  <a class="lang-card lang-ts" href="#/typescript/">
    <span class="lang-kicker">TypeScript</span>
    <strong>Types, generics, unions</strong>
    <span>Promises, arrays, modules</span>
  </a>
</div>

## C#

* [Syntax gotchas](/csharp/syntax.md) — `var`, interpolation, `nameof`, patterns
* [Null handling](/csharp/null-handling.md) — `??`, `??=`, `?.`, `is null`
* [Lambdas](/csharp/lambdas.md) — `Func`, `Action`, expression-bodied members
* [LINQ](/csharp/linq.md) — `Select`, `Where`, `FirstOrDefault`, `GroupBy`
* [async / await](/csharp/async.md) — `Task` basics and the usual pitfalls
* [Records](/csharp/records.md) — `init`, `with`, positional records
* [Collections](/csharp/collections.md) — `IEnumerable` and friends

## TypeScript

* [Types and narrowing](/typescript/types.md) — types, interfaces, unions
* [`?.` and `??`](/typescript/nullish.md) — optional chaining, nullish coalescing
* [Generics](/typescript/generics.md) — type parameters and constraints
* [Utility types](/typescript/utility-types.md) — `Partial`, `Pick`, `Omit`, `Record`, `Required`
* [Promises](/typescript/async.md) — `async` / `await` patterns
* [Array methods](/typescript/arrays.md) — `map`, `filter`, `reduce`, `find`
* [Discriminated unions](/typescript/discriminated-unions.md) — a shared literal tag
* [Modules](/typescript/modules.md) — import and export reminders

Snippets assume a current compiler: C# 10+ (a few notes call out C# 11) and TypeScript 5 with `strict` on.
