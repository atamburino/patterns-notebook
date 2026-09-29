# LINQ

`Where`, `Select`, and `GroupBy` build a query. Nothing runs until something enumerates it.

## Filter and map

```csharp
List<string> names = orders
    .Where(o => o.Total > 0)
    .Select(o => o.CustomerName)
    .ToList();
```

## First match

```csharp
Order? match = orders.FirstOrDefault(o => o.Id == id);
```

## Group

```csharp
var byCity = orders
    .GroupBy(o => o.City)
    .Select(g => new { City = g.Key, Count = g.Count() });
```

## Gotchas

- Deferred queries re-run on every enumeration. Call `ToList()` when the source is remote, expensive, or about to change.
- `First` throws when nothing matches. `FirstOrDefault` returns `default` — `null` for a class, `0` for `int`.
- `GroupBy` is lazy too. Materialize it if you walk the groups more than once.
