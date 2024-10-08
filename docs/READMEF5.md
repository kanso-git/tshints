In TypeScript, if you want to **extract the type** of a function's return value, you can use the built-in **`ReturnType<T>`** utility type. This type takes a function type `T` as a parameter and infers its return type.

### Using `ReturnType<T>`

The `ReturnType<T>` utility type helps you get the return type of a function.

#### Example 1: Basic Function Return Type Extraction

```typescript
function add(a: number, b: number) {
  return a + b // inferred return type: number
}

type AddReturnType = ReturnType<typeof add> // type AddReturnType = number

const result: AddReturnType = add(5, 3) // result is a number
```

- **`ReturnType<typeof add>`**: This extracts the return type of the `add` function, which in this case is `number`.

#### Example 2: Complex Function Return Type

If a function returns an object or array, you can still use `ReturnType` to infer its return type.

```typescript
function createUser(name: string, age: number) {
  return { name, age, active: true }
}

type UserType = ReturnType<typeof createUser>
// UserType is inferred as { name: string; age: number; active: boolean }

const user: UserType = createUser("Alice", 25) // correctly typed
```

- **`UserType`** is inferred as the return type of `createUser`, which is `{ name: string, age: number, active: boolean }`.

#### Example 3: Function Returning Another Function

When dealing with functions that return other functions, `ReturnType<T>` can help you extract the type of the returned function.

```typescript
function multiplyBy(factor: number) {
  return (x: number) => x * factor
}

type MultiplyByReturnType = ReturnType<typeof multiplyBy>
// MultiplyByReturnType is inferred as (x: number) => number

const doubler: MultiplyByReturnType = multiplyBy(2)
const result = doubler(5) // inferred as number (10)
```

- **`MultiplyByReturnType`** is inferred as `(x: number) => number`, which is the type of the function returned by `multiplyBy`.

#### Example 4: Async Function Return Type

If a function returns a `Promise`, `ReturnType<T>` will infer the type of the promise.

```typescript
async function fetchData() {
  return "Data fetched"
}

type FetchDataReturnType = ReturnType<typeof fetchData>
// FetchDataReturnType is inferred as Promise<string>

const dataPromise: FetchDataReturnType = fetchData()
```

- **`FetchDataReturnType`** is inferred as `Promise<string>`.

#### Example 5: Inferring Return Type from Anonymous Functions

You can use `ReturnType<T>` to infer the return type of anonymous or arrow functions.

```typescript
const square = (n: number) => n * n

type SquareReturnType = ReturnType<typeof square>
// SquareReturnType is inferred as number

const result: SquareReturnType = square(4) // result is a number
```

- **`SquareReturnType`** is inferred as `number` from the arrow function.

#### Example 6: Inferring Return Type from Method of an Object

You can use `ReturnType<T>` to infer the return type of a method from an object.

```typescript
const mathOperations = {
  multiply(a: number, b: number) {
    return a * b
  },
}

type MultiplyReturnType = ReturnType<typeof mathOperations.multiply>
// MultiplyReturnType is inferred as number

const result: MultiplyReturnType = mathOperations.multiply(2, 5) // result is a number
```

- **`MultiplyReturnType`** is inferred as the return type of the `multiply` method, which is `number`.

### Example 7: Conditional Return Type Inference (Advanced)

You can use **conditional types** in combination with `ReturnType` to infer different return types based on a condition.

```typescript
type ConditionalReturnType<T> = T extends (...args: any[]) => infer R
  ? R
  : never

function getName() {
  return "Alice"
}

type NameReturnType = ConditionalReturnType<typeof getName> // inferred as string
```

- **`ConditionalReturnType<T>`**: This is a custom type that extracts the return type (`R`) of a function `T`. It works similarly to `ReturnType<T>`, but gives you more control if needed.

### Example 8: Inferring Return Type of Overloaded Functions

For overloaded functions, `ReturnType<T>` will infer the return type of the **first matching overload**. TypeScript will pick the most suitable return type.

```typescript
function getValue(value: number): number
function getValue(value: string): string
function getValue(value: any): any {
  return value
}

type GetValueReturnType = ReturnType<typeof getValue> // inferred as any

const result: GetValueReturnType = getValue("Hello") // result is inferred as any
```

- In this case, `ReturnType<typeof getValue>` is inferred as `any` because `getValue` has multiple overloads with different return types.

### Summary:

- `ReturnType<T>` is a TypeScript utility type that extracts the return type of a function.
- It can infer return types for primitive values, objects, arrays, functions returning functions, and async functions.
- It works with anonymous and arrow functions, as well as class methods or object methods.
- For overloaded functions, it infers the return type of the most suitable overload.
