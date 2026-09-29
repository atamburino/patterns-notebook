# async / await

`async` lets you `await`. The method's real result is the `Task` it returns.

## A normal call

```csharp
public async Task<Order> GetOrderAsync(
    int id,
    CancellationToken ct)
{
    OrderDto dto = await client.GetAsync(id, ct);
    return Map(dto);
}
```

## Pass a task straight through

Use this when the method only returns another task. Keep `async` / `await` if you need `try` or `using` around the call — otherwise an exception thrown before a task exists escapes synchronously.

```csharp
public Task<Order> GetOrderAsync(int id, CancellationToken ct)
    => client.GetAsync(id, ct);
```

## Gotchas

- `async void` is for event handlers. Anywhere else you cannot `await` it, and exceptions escape the method.
- `.Result` and `.Wait()` block a thread. On UI apps and classic ASP.NET they can deadlock. `await` instead.
- `await` does not cancel work by itself. Pass the `CancellationToken` into the call that accepts one.
