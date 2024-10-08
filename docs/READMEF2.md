In TypeScript, function annotations (also known as type annotations) can be used to specify the types of the parameters and the return value of a function. Here's how to annotate a function for various types of parameters and return types:

### 1. **Basic Function Annotations**

You can annotate the types of the function's parameters and return type:

```typescript
function add(a: number, b: number): number {
  return a + b
}
```

- **Parameters**: `a` and `b` are both `number`.
- **Return type**: The function returns a `number`.

### 2. **Function with Multiple Parameter Types**

You can specify different types for different parameters:

```typescript
function logMessage(message: string, count: number): void {
  console.log(`${message} repeated ${count} times`)
}
```

- **Parameters**: `message` is a `string`, and `count` is a `number`.
- **Return type**: `void` because it doesn't return anything.

### 3. **Function with Optional Parameters**

You can mark a parameter as optional by adding a `?` after the parameter name:

```typescript
function greet(name: string, age?: number): string {
  if (age) {
    return `Hello, ${name}. You are ${age} years old.`
  }
  return `Hello, ${name}.`
}
```

- **`age`** is optional and can either be a `number` or `undefined`.

### 4. **Function with Default Parameters**

You can provide default values for parameters:

```typescript
function multiply(a: number, b: number = 1): number {
  return a * b
}
```

- **`b`** is optional with a default value of `1`.

### 5. **Function with Union Types**

Parameters can accept more than one type using union types (`|`):

```typescript
function printId(id: number | string): void {
  console.log(`Your ID is: ${id}`)
}
```

- **Parameter**: `id` can either be a `number` or a `string`.

### 6. **Function with Rest Parameters**

You can use rest parameters to accept a variable number of arguments:

```typescript
function sum(...numbers: number[]): number {
  return numbers.reduce((acc, curr) => acc + curr, 0)
}
```

- **Rest Parameter**: `...numbers` accepts an array of `number`s.

### 7. **Function as a Type**

You can define a function type separately and then use it:

```typescript
type MathOperation = (a: number, b: number) => number

const multiply: MathOperation = (a, b) => a * b
```

- **`MathOperation`** is a function type that takes two `number` parameters and returns a `number`.

### 8. **Anonymous Functions**

You can annotate anonymous functions (e.g., arrow functions) in TypeScript:

```typescript
const divide = (a: number, b: number): number => {
  return a / b
}
```

### 9. **Function with Generic Types**

If your function can work with various types, you can use **generics**:

```typescript
function identity<T>(arg: T): T {
  return arg
}

const result = identity<string>("Hello") // Explicit generic
const numResult = identity(10) // Implicit generic
```

- **Generics**: `T` is a placeholder for a type, which is specified when calling the function.

### 10. **Return Type Inference**

TypeScript can automatically infer the return type if you don't specify it explicitly:

```typescript
function subtract(a: number, b: number) {
  return a - b // TypeScript infers return type as number
}
```

### Full Example Covering All Types

```typescript
// Function with various types
function processInput<T>(
  input: T,
  shouldLog: boolean = false,
  count?: number
): string | T[] {
  if (shouldLog) {
    console.log(input)
  }

  if (count !== undefined) {
    return new Array(count).fill(input)
  }

  return `Processed: ${input}`
}

// Using the function
let result1 = processInput("Hello", true) // Logs and returns string
let result2 = processInput(42, false, 3) // Returns an array [42, 42, 42]
```

This example shows how to combine different TypeScript features like default parameters, optional parameters, generics, and union types.

### Summary:

- **Parameters**: Annotate with types such as `number`, `string`, `boolean`, etc.
- **Return Type**: Specify the type after the parameter list.
- **Optional Parameters**: Use `?`.
- **Default Parameters**: Provide default values.
- **Union Types**: Use `|`.
- **Rest Parameters**: Use `...`.
- **Generics**: Use `<T>` to make functions flexible for various types.
