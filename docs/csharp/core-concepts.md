# Core concepts

Short notes on the C# that usually shows up around a service method.

## Namespaces

A namespace is a name prefix so types do not collide. It usually matches the folder path. The compiler does not check the folder. Only the `namespace` line matters.

```csharp
namespace Billing.Invoices;

public sealed class InvoiceWriter { }
```

## Sealed classes and records

`sealed` blocks inheritance. A `record` compares by value, so two instances with the same data are equal.

```csharp
public sealed class TokenStore { }

public sealed record Row(string? Value, string? Error);

var left = new Row("ok", null);
var right = new Row("ok", null);
bool same = left == right; // true
```

More on records: [Records](/csharp/records.md).

## Nullable `?`

`?` allows null. Return null for a normal "no result." Throw when the failure is unexpected.

```csharp
User? Find(int id) => store.TryGet(id); // null means not found

User Require(int id) =>
    store.TryGet(id) ?? throw new InvalidOperationException("missing user");
```

## Static factory methods

A static method on the record names the outcome and fills the right slots.

```csharp
public sealed record Row(string? Value, string? Error)
{
    public static Row Succeeded(string row) => new Row(row, null);
    public static Row Failed(string error) => new Row(null, error);
}
```

## Null-forgiving `!`

`!` only silences the compiler warning. It does not check null at runtime. A real null still throws when you use the value.

```csharp
string email = user.Email!; // warning gone
email.ToUpper();             // NullReferenceException if Email is null
```

Null checks that actually branch: [Null handling](/csharp/null-handling.md).

## Constructor injection

The class lists what it needs in the constructor. The host passes the implementations in.

```csharp
public sealed class RowService
{
    private readonly IConnectionsApi _connections;
    private readonly ITypeValueProvider _types;
    private readonly IHttpContextAccessor _http;
    private readonly ILogger<RowService> _logger;

    public RowService(
        IConnectionsApi connections,
        ITypeValueProvider types,
        IHttpContextAccessor http,
        ILogger<RowService> logger)
    {
        _connections = connections;
        _types = types;
        _http = http;
        _logger = logger;
    }
}
```

## `??` and `??=`

`??` picks the right side when the left side is null. `??=` writes that fallback back only in the same case.

```csharp
Task delay = deleteRetryDelay ?? Task.Delay(TimeSpan.FromSeconds(1), ct);

deleteRetryDelay ??= Task.Delay(TimeSpan.FromSeconds(1), ct);
```

## Arrow functions

A lambda is a tiny function with no name. Inputs sit left of `=>`. The result sits on the right.

```csharp
Func<int, int> twice = x => x * 2;
```

`Func`, `Action`, and expression-bodied members: [Lambdas](/csharp/lambdas.md).

## LINQ `Select`

`Select` is a method on `IEnumerable<T>` from the framework (`using System.Linq`). When something enumerates the sequence, it walks each item and applies the lambda.

```csharp
using System.Linq;

IEnumerable<int> doubled = numbers.Select(x => x * 2);
```

`Where`, `FirstOrDefault`, and deferred execution: [LINQ](/csharp/linq.md).

## Fail-fast validation

Check required fields before any real work. Return a failed result, or `401`, and stop.

```csharp
public IActionResult Delete(string? id)
{
    if (string.IsNullOrWhiteSpace(id))
        return BadRequest(Row.Failed("id is required"));

    if (User.Identity?.IsAuthenticated != true)
        return Unauthorized(); // 401

    return Ok(_connections.Delete(id));
}
```

## `async` and `CancellationToken`

`await` waits. It does not cancel. Pass the token into every call that accepts one, and check it before you start work.

```csharp
public async Task<Row> DeleteAsync(string id, CancellationToken ct)
{
    ct.ThrowIfCancellationRequested();
    await Task.Delay(retryDelay, ct);
    return await _connections.DeleteAsync(id, ct);
}
```

Tasks and the blocking pitfalls: [async / await](/csharp/async.md).

## Gotchas

- Moving a file does not change its namespace. The declaration and the folder can drift apart.
- `sealed` stops subclasses. It does not freeze the object's fields.
- `!` is not a fallback. Use `??` when you want another value, and `is null` when you want a branch.
- `??` and `??=` skip the right-hand side when the left side is already non-null. An empty string is not null, so it is kept.
- `Select` does not run the lambda until the sequence is enumerated.
- A `CancellationToken` dropped on one hop leaves that hop running after the caller has stopped.
