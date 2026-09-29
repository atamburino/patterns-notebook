# Array methods

`map`, `filter`, and `reduce` return something new. They do not change the input array.

```ts
const names = users.map((u) => u.name);
const active = users.filter((u) => u.active);
const total = orders.reduce((sum, o) => sum + o.total, 0);
const match = users.find((u) => u.id === id);
```

## Gotchas

- `find` returns the element or `undefined`. `filter` returns an array, which may be empty.
- Always pass an initial value to `reduce`. An empty array with no initial value throws.
- `forEach` ignores a returned promise. For sequential `await`, use `for...of`.
