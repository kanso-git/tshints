In TypeScript, the `in keyof` and `extends` keywords are both used in different contexts but serve distinct purposes in the type system. Below is an explanation of each along with examples to clarify their differences.

### 1. **`in keyof`: Iterating over Keys of a Type**

The `in keyof` construct is commonly used in **mapped types** to iterate over the keys of an object or type. It allows you to loop through the keys of a type and create a new type based on those keys.

#### Example: `in keyof` in Mapped Types

```typescript
type Person = {
  name: string
  age: number
  location: string
}

type ReadOnlyPerson = {
  readonly [K in keyof Person]: Person[K]
}
```

In this example:

- **`keyof Person`**: Produces a union type of the keys of `Person`, which is `"name" | "age" | "location"`.
- **`in keyof Person`**: Iterates over these keys (`"name"`, `"age"`, `"location"`) and creates a new type by transforming each key.
- **Mapped Type**: It creates a new type (`ReadOnlyPerson`) where each property in `Person` becomes `readonly`.

### Explanation:

- **`keyof`**: When used, `keyof` turns the keys of a type into a union of literal types.
- **`in keyof`**: It is used inside a mapped type to iterate over the keys of a type.

#### Use Case: Mapped Types with `in keyof`

```typescript
type OptionalPerson = {
  [K in keyof Person]?: Person[K]
}

// OptionalPerson is equivalent to:
// {
//     name?: string;
//     age?: number;
//     location?: string;
// }
```

Here, the **`in keyof`** iterates over the keys of `Person` and makes them all optional (`?`).

### 2. **`extends`: Type Constraints and Conditional Types**

The `extends` keyword is used in two main contexts:

- **Type Constraints**: To define type parameters that must satisfy certain conditions (usually in generics).
- **Conditional Types**: To conditionally infer one type based on another.

#### A. **`extends` for Type Constraints**

In generic types or functions, `extends` ensures that a type parameter is constrained to a specific type or structure.

```typescript
function logLength<T extends { length: number }>(arg: T): void {
  console.log(arg.length)
}

logLength("Hello") // Works because string has a length property
logLength([1, 2, 3]) // Works because array has a length property
```

In this example:

- **`T extends { length: number }`**: This constrains `T` to be any type that has a `length` property. Only types that satisfy this constraint (like arrays, strings, etc.) are allowed.

#### B. **`extends` for Conditional Types**

Conditional types allow you to choose one type based on whether a type extends another.

```typescript
type IsString<T> = T extends string ? "string" : "not string"

type Test1 = IsString<string> // "string"
type Test2 = IsString<number> // "not string"
```

In this example:

- **`T extends string`**: This is a conditional type that checks if `T` is assignable to `string`. If so, it returns `"string"`, otherwise `"not string"`.

#### Use Case: Combining `extends` and `keyof`

```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key]
}

const person = { name: "Alice", age: 25 }
const name = getProperty(person, "name") // "Alice", inferred as string
```

Here:

- **`K extends keyof T`**: Ensures that `K` is a valid key of `T`, meaning you can only access properties that exist on `T`.

### **Key Differences Between `in keyof` and `extends`**

| Feature                 | `in keyof`                                                                                                    | `extends`                                                                                         |
| ----------------------- | ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| **Purpose**             | Iterates over the keys of a type in mapped types.                                                             | Constrains or checks if a type is assignable to another type.                                     |
| **Common Use Cases**    | - Mapped types<br> - Transforming types<br> - Making properties optional, readonly, or modifying their types. | - Type constraints in generics<br> - Conditional types<br> - Inference and narrowing of types.    |
| **Example**             | `type ReadOnly<T> = { readonly [K in keyof T]: T[K] };`                                                       | `function foo<T extends string>(arg: T): void {}`                                                 |
| **Iterates Over Keys?** | Yes, iterates over keys using `in keyof`.                                                                     | No, it checks type relationships or constraints.                                                  |
| **Type Relation**       | `keyof` generates a union of keys. The `in` operator iterates over the keys to transform types.               | `extends` checks if one type is a subtype of another, often used for constraints or conditionals. |

### Conclusion

- **`in keyof`** is used to iterate over the keys of an object type, typically in the context of **mapped types**.
- **`extends`** is used to apply **type constraints** (such as in generics) or to implement **conditional types** that depend on whether one type is assignable to another.

Both are powerful tools in TypeScript’s type system but serve distinct purposes: `in keyof` focuses on transforming types based on their keys, while `extends` is used to enforce or check type relationships.
