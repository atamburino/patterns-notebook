# Modules

Prefer named exports. They search, rename, and tree-shake more predictably than `export default`.

## Export

```ts
export interface User {
  id: string;
  name: string;
}

export function label(user: User): string {
  return user.name;
}
```

## Import

```ts
import { label, type User } from "./user.js";
```

## Gotchas

- `import { type User }` (or `import type`) is erased. Use it so a types-only file does not become a runtime import.
- With `"module": "nodenext"` (`moduleResolution` `nodenext` or `node16`), a relative import uses the runtime specifier, including `.js`, even though the file you edit is `.ts`.
- `export default` creates one anonymous export. Named exports stay greppable when the module grows.
