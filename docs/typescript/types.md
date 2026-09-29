# Types and narrowing

Interfaces describe object shapes. Type aliases can also name unions, tuples, and primitives.

## Interface and type

```ts
interface User {
  id: string;
  name: string;
}

type Id = string | number;
```

## A union

```ts
type Result =
  | { ok: true; value: string }
  | { ok: false; error: string };
```

## Narrow before you use it

```ts
function label(id: Id): string {
  if (typeof id === "string") return id.toUpperCase();
  return `#${id}`;
}
```

## Gotchas

- Interfaces merge: a second `interface User` adds members. A second `type User` is an error. Prefer `type` for unions.
- A union has only the members shared by every arm until you narrow with `typeof`, `in`, `instanceof`, or a discriminant.
- Extra properties are checked on object literals assigned directly to a type. They are not checked once the value has already been widened.
