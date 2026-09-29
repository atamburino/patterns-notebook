# Records

Records are types with value-based equality. `init` closes a property after construction. `with` copies, then patches.

## Positional record

```csharp
public record Order(int Id, string City);

Order moved = order with { City = "Austin" };
```

## Init and required

```csharp
public record Customer
{
    public required string Name { get; init; }
    public string? City { get; init; }
}

var customer = new Customer { Name = "Ada" };
```

## Gotchas

- `with` is a shallow copy. Nested objects are shared with the original.
- `record` means `record class` (a reference type). `record struct` is a value type with different copying behavior.
- `required` is C# 11. `init` and `with` arrived with records in C# 9. `init` can still be bypassed by reflection or by code inside the type.
