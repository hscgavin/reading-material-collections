## Advanced Typescript by Examples

### 1. keyof

Similar to `Object.keys`, but it's used in interface

```ts
interface Student {
    name: string;
    age: number;
}

// type keys = "name" | "age"
type keys = keyof Student;

```

For some typescript beginners they probably would write a following `get` function at the beginning:

```ts
const student = {
  name: 'Jon Snow',
  age: 30
}

function get(s: object, k: string) {
  return s[k];
}
```
But it has some disadvantages:

1. Unable to confirm the return type: this will lose the maximum type checking function of ts
2. Unable to constrain key: you may make spelling mistakes

That's where `keyof` comes in, you can use it with other parts of the type system to get type-safe lookups:

```ts
function get<T extends object, K extends keyof T>(s: T, k: K): T[K] {
  return s[k]
}
```
