# Discriminated unions

Give every member the same property, with a unique literal type. Switch on that property and the other fields narrow.

```ts
type Shape =
  | { kind: "circle"; radius: number }
  | { kind: "rect"; width: number; height: number };

function area(shape: Shape): number {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "rect":
      return shape.width * shape.height;
  }
}
```

## Exhaustiveness

```ts
function assertNever(value: never): never {
  throw new Error(`Unexpected ${JSON.stringify(value)}`);
}
```

Add `default: return assertNever(shape)` when a missed `kind` should be a compile error.

## Gotchas

- The tag has to be a literal (`"circle"`), not `string`. Otherwise the arms do not narrow.
- Every member needs the tag. An optional `kind?` breaks the discrimination.
- A `default` that returns `never` fails the build when a new member is added and the switch is not updated.
