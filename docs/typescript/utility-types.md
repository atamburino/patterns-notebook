# Utility types

Built-in object rewrites. All five below are shallow.

```ts
interface User {
  id: string;
  name: string;
  email: string;
}

type UserPatch = Partial<User>;
type PublicUser = Pick<User, "id" | "name">;
type WithoutEmail = Omit<User, "email">;
type ById = Record<string, User>;
type Complete = Required<User>;
```

## Gotchas

- `Partial<T>` and `Required<T>` change one level. A nested object keeps its own required and optional fields.
- `Required<T>` removes `?`. It does not remove `null` from `string | null`.
- `Record<string, User>` is an index signature. TypeScript will still allow any string key, not only keys you have already filled in.
