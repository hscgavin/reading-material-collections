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


### 1. Required, Partial & Pick

Now we understand of the usage of `keyof`, let's dive into a few of utility types provided by typescript.

It's import for us to understand how they leverage `keyof`:

```ts
// Constructs a type with all properties of T set to optional.
type Partial<T> = {
  [P in keyof T]?: T[P];
};

type Required<T> = {
  // -? means must be all present,
  // aka it removes optionality (?) 
  [P in keyof T]-?: T[P];
};
// Constructs a type by picking the set of properties K from T.
type Pick<T, K extends keyof T> = {
  [P in K]: T[P];
};

interface Student {
  id: number;
  email: string;
  name: string;
};

// { id?: number; email?: string; name?: string; }
type PartialStudent = Partial<Student>

// { name: string; email: string; }
type PickStudent = Pick<User, "string" | "email">

```