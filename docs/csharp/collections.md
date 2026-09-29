# Collections

Pick the type that matches how you use the data, and treat `IEnumerable<T>` as "you may enumerate this," not "this is a snapshot."

## Query vs snapshot

```csharp
IEnumerable<int> query = nums.Where(n => n > 0);
IReadOnlyList<int> snapshot = query.ToList();
```

## Lookup

```csharp
Dictionary<int, Order> byId =
    orders.ToDictionary(o => o.Id);

if (byId.TryGetValue(id, out Order? order))
{
    Use(order);
}
```

## Gotchas

- Enumerating an `IEnumerable<T>` twice re-runs the work. That includes a second `foreach`, or `Count()` followed by `foreach`.
- `ToDictionary` throws if two items share a key. Group first when keys are not unique.
- Return `IReadOnlyList<T>` from an API when the caller should read and index but not mutate. Keep `List<T>` for code that adds items.
