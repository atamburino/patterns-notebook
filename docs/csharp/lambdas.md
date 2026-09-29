# Lambdas

`Func` returns a value. `Action` does not. Expression-bodied members are a single expression.

## Delegates

```csharp
Func<int, int, int> add = (a, b) => a + b;
Action<string> log = msg => Console.WriteLine(msg);
Func<int, bool> isEven = static n => n % 2 == 0;
```

## Expression-bodied members

```csharp
int Twice(int n) => n * 2;

string Label => $"{Id}:{Name}";

void Save() => store.Write(this);
```

## Gotchas

- `Predicate<T>` is logically `Func<T, bool>`, but it is a different delegate type. You cannot pass one where the other is required without a wrapper.
- A `static` lambda cannot capture locals. Use it when you want the compiler to reject an accidental closure.
- Expression-bodied members have no statement block. If you need `if` as a statement or more than one line, use braces.
