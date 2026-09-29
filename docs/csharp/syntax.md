# Syntax gotchas

Small C# forms that are easy to half-remember.

## `var` vs explicit

`var` is inferred and still static. It is not `dynamic`.

```csharp
var count = 3; // int
List<Order> orders = GetOrders();
var id = order.Id;
```

## Interpolation

```csharp
string label = $"{user.Name} ({user.Id})";
string padded = $"{total,8:0.00}";
string braces = $"{{ \"id\": {user.Id} }}";
```

## `nameof`

```csharp
throw new ArgumentNullException(nameof(user));
string prop = nameof(Order.Total); // "Total"
```

## Pattern matching

```csharp
if (shape is Circle { Radius: > 0 } c)
{
    return Math.PI * c.Radius * c.Radius;
}

string desc = n switch
{
    0 => "empty",
    > 0 and < 10 => "small",
    _ => "other"
};
```

## Gotchas

- Prefer `var` when the right-hand side shows the type (`new`, a cast, a literal). Prefer an explicit type when a method call hides it.
- `nameof` does not read the value. `nameof(Order.Total)` is `"Total"`, not `"Order.Total"`.
- A pattern variable such as `c` exists only on the match path. `_` in a switch expression is the discard arm, not a variable.
