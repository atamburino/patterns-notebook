# `?.` and `??`

Optional chaining stops on `null` or `undefined`. Nullish coalescing replaces only those two values.

## Read a chain

```ts
const city = order?.shipTo?.city ?? "unknown";
const count = options.count ?? 10;
```

## `??` is not `||`

```ts
const title = input.title ?? "Untitled"; // nullish only
const fallback = input.title || "Untitled"; // also "", 0, false
```

## Gotchas

- `?.` yields `undefined` when it stops. It does not yield `null` unless that was already the value you read.
- `??` leaves `""`, `0`, and `false` alone. Reach for `||` only when those should count as missing.
- Mixing `??` and `||` without parentheses is a syntax error. Write `(a ?? b) || c`.
