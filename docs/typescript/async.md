# Promises

An `async` function always returns a promise. A thrown error becomes a rejection.

## Await one call

```ts
async function loadUser(id: string): Promise<User> {
  const res = await fetch(`/api/users/${id}`);
  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  return (await res.json()) as User;
}
```

## Await several

```ts
const [user, orders] = await Promise.all([
  loadUser(id),
  loadOrders(id),
]);
```

## Gotchas

- `Promise.all` rejects when any input rejects. Use `Promise.allSettled` when you need every result anyway.
- A call without `await` (or without `.catch`) is a floating promise. Its rejection is easy to miss.
- `as User` tells the compiler to trust you. It does not check the JSON.
