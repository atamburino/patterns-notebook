# Generics

A type parameter is filled in by the caller. Constraints limit what they may pass.

## A simple parameter

```ts
function first<T>(items: readonly T[]): T | undefined {
  return items[0];
}
```

## Keep the key and the value linked

```ts
function pluck<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}
```

## Constrain the shape

```ts
interface Repo<T extends { id: string }> {
  get(id: string): Promise<T | undefined>;
}
```

## Gotchas

- Generics are erased. You cannot write `new T()` unless the caller also passes a constructor.
- `K extends keyof T` is what makes `obj[key]` return `T[K]` instead of a union of every property.
- If the function truly does not care what the value is, take `unknown` and narrow it. `any` turns checking off.
