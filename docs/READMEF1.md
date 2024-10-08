You can use **generics** with arrow functions in TypeScript just like with regular functions. The generic type is placed before the parameter list and is used within the function body. Here's how to do it:

### Basic Example of an Arrow Function with Generics

```typescript
const identity = <T>(arg: T): T => {
  return arg
}
```

- **`<T>`**: This is the generic type parameter, which allows the function to work with any type.
- **`arg: T`**: The function accepts a parameter `arg` of type `T`.
- **Return type**: The function returns the same type `T`.

### Example Usage

```typescript
let stringOutput = identity<string>("Hello") // Explicitly setting the generic type
let numberOutput = identity(42) // TypeScript infers the generic type
```

In the first case, we explicitly specify the generic type as `string`. In the second case, TypeScript infers the type from the argument.

### Arrow Function with Multiple Generic Types

You can use multiple generic types in an arrow function:

```typescript
const mergeObjects = <T, U>(obj1: T, obj2: U): T & U => {
  return { ...obj1, ...obj2 }
}
```

- **`<T, U>`**: We define two generic types, `T` and `U`.
- **Parameters**: `obj1` has type `T`, and `obj2` has type `U`.
- **Return type**: The function returns an object that combines both types (`T & U`).

### Example Usage

```typescript
const person = { name: "John" }
const details = { age: 30 }

const merged = mergeObjects(person, details)
// merged is inferred as { name: string; age: number; }
```

### Generic Arrow Function with Default Parameters

You can also use default parameters with generic arrow functions:

```typescript
const createArray = <T>(value: T, count: number = 1): T[] => {
  return new Array(count).fill(value)
}
```

### Example Usage

```typescript
const array1 = createArray<string>("Hello", 3) // ['Hello', 'Hello', 'Hello']
const array2 = createArray<number>(42) // [42] (default count is 1)
```

### Arrow Function with Rest Parameters and Generics

You can use **rest parameters** with generics in arrow functions:

```typescript
const logValues = <T>(...values: T[]): void => {
  values.forEach((value) => console.log(value))
}
```

- **Rest Parameter**: `...values` allows an arbitrary number of arguments of type `T[]`.
- **Return Type**: The function doesn't return anything, so its return type is `void`.

### Example Usage

```typescript
logValues<number>(1, 2, 3, 4) // Logs: 1, 2, 3, 4
logValues<string>("a", "b", "c") // Logs: a, b, c
```

### Summary:

- You can use generics in arrow functions by placing the generic type parameter (`<T>`, `<T, U>`, etc.) before the parameter list.
- The generic type can be used for parameter types, return types, and within the function body.
- TypeScript will infer the generic type if it can, or you can specify it explicitly when calling the function.
