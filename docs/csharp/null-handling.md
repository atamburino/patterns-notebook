# Null handling

`??`, `??=`, and `?.` only care about null. Empty string, `0`, and `false` pass through.

## Coalesce and assign

```csharp
string name = user.Name ?? "anonymous";
name ??= "anonymous"; // assign only when null

string city = order?.ShipTo?.City ?? "unknown";
int? length = user?.Name?.Length;
```

## Null checks

```csharp
if (value is null)
{
    return;
}

if (value is not null)
{
    Use(value);
}
```

## Gotchas

- `?.` stops the chain and yields null. On a value-type member such as `Length`, the result is lifted to `int?`.
- `??=` does not evaluate the right-hand side when the left side is already non-null.
- Prefer `is null` / `is not null` over `== null` when a type might overload `==`.
