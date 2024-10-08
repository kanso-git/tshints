In TypeScript, Type Inference is a feature that allows TypeScript to automatically deduce the type of a value based on how it is used. For functions, TypeScript can infer the return type based on the return statement of the function, without you having to explicitly annotate it.

Here are multiple examples demonstrating how TypeScript infers types from function returns:

### 1. **Simple Inference from Primitive Types**

When a function returns a basic primitive type (e.g., `string`, `number`, `boolean`), TypeScript automatically infers the return type based on the return value.

```typescript
function add(a: number, b: number) {
  return a + b // inferred return type: number
}

function greet(name: string) {
  return `Hello, ${name}!` // inferred return type: string
}

const result1 = add(5, 3) // inferred type: number
const result2 = greet("Alice") // inferred type: string
```

- **`add`**: Inferred return type is `number`.
- **`greet`**: Inferred return type is `string`.

### 2. **Inference from Objects**

If a function returns an object, TypeScript infers the return type based on the shape of the object.

```typescript
function createUser(name: string, age: number) {
  return { name, age } // inferred return type: { name: string, age: number }
}

const user = createUser("Alice", 25)
// user is inferred as { name: string, age: number }
```

- TypeScript infers that the function returns an object with `name` as a `string` and `age` as a `number`.

### 3. **Inference from Arrays**

When a function returns an array, TypeScript infers the return type as an array of the inferred element type.

```typescript
function getNumbers() {
  return [1, 2, 3] // inferred return type: number[]
}

function getStrings() {
  return ["a", "b", "c"] // inferred return type: string[]
}

const numbers = getNumbers() // inferred as number[]
const strings = getStrings() // inferred as string[]
```

- **`getNumbers`**: Inferred as `number[]`.
- **`getStrings`**: Inferred as `string[]`.

### 4. **Inference from Union Types**

When a function returns different types based on some logic, TypeScript will infer the return type as a **union** of the possible types.

```typescript
function randomResult() {
  if (Math.random() > 0.5) {
    return "Success" // string
  } else {
    return 42 // number
  }
}

const result = randomResult() // inferred as string | number
```

- The return type of **`randomResult`** is inferred as `string | number` because both `string` and `number` are possible return values.

### 5. **Inference from Conditional Statements**

TypeScript infers the return type even when the function has conditional branches.

```typescript
function isEven(num: number) {
  if (num % 2 === 0) {
    return true // boolean
  } else {
    return false // boolean
  }
}

const isNumEven = isEven(4) // inferred as boolean
```

- The return type of **`isEven`** is inferred as `boolean`, because both branches return a `boolean`.

### 6. **Inference from Functions Returning Functions**

When a function returns another function, TypeScript infers the type of the returned function as well.

```typescript
function multiplyBy(factor: number) {
  return (x: number) => x * factor // inferred return type: (x: number) => number
}

const doubler = multiplyBy(2)
const result = doubler(5) // inferred as number (5 * 2 = 10)
```

- **`multiplyBy`** returns a function, and TypeScript infers the returned function’s type as `(x: number) => number`.

### 7. **Inference with Promises**

If a function returns a `Promise`, TypeScript infers the type wrapped by the `Promise`.

```typescript
function fetchData() {
  return new Promise<string>((resolve) => {
    resolve("Data fetched")
  })
}

const dataPromise = fetchData() // inferred as Promise<string>
```

- **`fetchData`** returns a `Promise<string>`, inferred automatically by TypeScript.

### 8. **Inference with Generics**

Generics allow you to create functions where TypeScript can infer the type based on the argument passed to the function.

```typescript
function identity<T>(value: T) {
  return value // inferred return type: T
}

const str = identity("Hello") // inferred as string
const num = identity(123) // inferred as number
const bool = identity(true) // inferred as boolean
```

- **`identity`** is a generic function, and TypeScript infers the return type based on the type of the argument.

### 9. **Inference with Destructuring**

TypeScript can also infer types from destructuring return values.

```typescript
function getCoordinates() {
  return { x: 10, y: 20 } // inferred return type: { x: number, y: number }
}

const { x, y } = getCoordinates() // x inferred as number, y inferred as number
```

- **`getCoordinates`** returns an object with `x` and `y`, both of which are inferred as `number`.

### 10. **Inference in Asynchronous Functions (`async/await`)**

In `async` functions, TypeScript infers the return type as a `Promise` wrapping the inferred type of the `await` expression.

```typescript
async function getData() {
  return "Hello" // inferred return type: Promise<string>
}

async function fetchNumber() {
  return 42 // inferred return type: Promise<number>
}

const data = await getData() // inferred as string
const number = await fetchNumber() // inferred as number
```

- TypeScript infers `Promise<string>` for `getData()` and `Promise<number>` for `fetchNumber()`.

### 11. **Complex Inference with Nested Functions**

TypeScript can infer types even for nested functions or callbacks.

```typescript
function operate(operation: (x: number, y: number) => number) {
  return operation(10, 5)
}

const result = operate((a, b) => a + b) // inferred as number
```

- In the example above, TypeScript infers that the return value is a `number` based on the signature of the `operation` function.

### 12. **Inference with Type Aliases or Interfaces**

TypeScript can infer the return type when you use a type alias or interface.

```typescript
type User = { name: string; age: number }

function getUser() {
  return { name: "Alice", age: 25 } // inferred return type: User
}

const user = getUser() // inferred as User
```

- The return type is inferred as `{ name: string; age: number; }`, which is structurally equivalent to the `User` type.

### Summary:

- TypeScript automatically infers the return type of a function based on its `return` statement.
- For simple primitives, objects, arrays, and more complex types like unions and functions, TypeScript will deduce the appropriate type.
- In more complex scenarios like returning promises, generics, or nested functions, TypeScript still correctly infers the return type based on the function’s logic.
