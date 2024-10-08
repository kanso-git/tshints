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

const result = identity<string>('Hello') // Explicit generic
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
let result1 = processInput('Hello', true) // Logs and returns string
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
let stringOutput = identity<string>('Hello') // Explicitly setting the generic type
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
const person = { name: 'John' }
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
const array1 = createArray<string>('Hello', 3) // ['Hello', 'Hello', 'Hello']
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
logValues<string>('a', 'b', 'c') // Logs: a, b, c
```

### Summary:

- You can use generics in arrow functions by placing the generic type parameter (`<T>`, `<T, U>`, etc.) before the parameter list.
- The generic type can be used for parameter types, return types, and within the function body.
- TypeScript will infer the generic type if it can, or you can specify it explicitly when calling the function.

In TypeScript, you can work with **type instances of another type** and define more **complex types** using **generics**, **mapped types**, **conditional types**, and **utility types**. These constructs allow you to create types that depend on or are based on other types.

### 1. **Type Instance of Another Type (Generics)**

Generics are the primary tool for creating types that depend on other types. You can create a type where one type is based on another type's instance.

#### Example: Creating a Wrapper Type

```typescript
type Box<T> = {
  value: T
}

const stringBox: Box<string> = { value: 'Hello' }
const numberBox: Box<number> = { value: 123 }
```

- **`Box<T>`**: This generic type represents a "box" containing a value of type `T`.
- **`stringBox`** and **`numberBox`** are instances of the `Box` type, specialized for `string` and `number`, respectively.

### 2. **Type Instance of Another Type (Mapped Types)**

Mapped types allow you to create a new type by transforming properties of another type.

#### Example: Mapping Over Properties of Another Type

```typescript
type ReadonlyType<T> = {
  readonly [K in keyof T]: T[K]
}

type Person = {
  name: string
  age: number
}

const readonlyPerson: ReadonlyType<Person> = {
  name: 'Alice',
  age: 25,
}

// readonlyPerson.name = "Bob"; // Error: Cannot assign to 'name' because it is a read-only property
```

- **`ReadonlyType<T>`**: A mapped type that makes all properties of type `T` `readonly`.
- **`keyof T`**: This is used to iterate over the keys of the type `T` to transform each property.

### 3. **Conditional Types**

Conditional types allow you to create types that depend on a condition evaluated at the type level.

#### Example: Type Based on Conditional Logic

```typescript
type IsString<T> = T extends string ? 'string' : 'not string'

type Test1 = IsString<string> // "string"
type Test2 = IsString<number> // "not string"
```

- **`IsString<T>`**: This type checks if `T` extends `string`. If `T` is a `string`, it resolves to `"string"`, otherwise `"not string"`.

### 4. **Extracting Subtypes**

You can use **conditional types** to extract specific properties or subtypes from a more complex type.

#### Example: Extract Properties of a Certain Type

```typescript
type ExtractStringProperties<T> = {
  [K in keyof T]: T[K] extends string ? K : never
}[keyof T]

type User = {
  name: string
  age: number
  email: string
}

type StringKeys = ExtractStringProperties<User> // "name" | "email"
```

- **`ExtractStringProperties<T>`**: This mapped type extracts keys whose value types are `string`.

### 5. **Utility Types**

TypeScript provides several **utility types** that operate on other types to create more complex types.

#### Common Utility Types

- **`Partial<T>`**: Makes all properties of `T` optional.
- **`Required<T>`**: Makes all properties of `T` required.
- **`Readonly<T>`**: Makes all properties of `T` readonly.
- **`Record<K, T>`**: Creates an object type with keys of type `K` and values of type `T`.
- **`Pick<T, K>`**: Creates a type by picking a set of properties from `T`.
- **`Omit<T, K>`**: Creates a type by omitting a set of properties from `T`.

#### Example: Combining Utility Types

```typescript
type User = {
  name: string
  age: number
  email: string
}

// Partial user
type PartialUser = Partial<User>

// Readonly user
type ReadonlyUser = Readonly<User>

// Pick only name and email
type UserNameAndEmail = Pick<User, 'name' | 'email'>

// Omit age from User
type UserWithoutAge = Omit<User, 'age'>
```

### 6. **Type Inference with Generics**

You can infer types dynamically when using generic functions.

#### Example: Inferring Types from Function Parameters

```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key]
}

const person = { name: 'John', age: 30 }

const name = getProperty(person, 'name') // string
const age = getProperty(person, 'age') // number
```

- **`K extends keyof T`**: This ensures that the `key` parameter is a valid property key of `T`.
- The return type is dynamically inferred based on the type of the property accessed.

### 7. **Complex Example Combining Various Concepts**

#### Example: A Function Returning a Conditional Type

```typescript
type Admin = {
  role: 'admin'
  permissions: string[]
}

type Guest = {
  role: 'guest'
  visitCount: number
}

type User = Admin | Guest

type GetUserRole<T extends User> = T extends Admin ? 'Admin' : 'Guest'

function getUserRole<T extends User>(user: T): GetUserRole<T> {
  if (user.role === 'admin') {
    return 'Admin' as GetUserRole<T>
  }
  return 'Guest' as GetUserRole<T>
}

const adminUser: Admin = { role: 'admin', permissions: ['read', 'write'] }
const guestUser: Guest = { role: 'guest', visitCount: 5 }

const adminRole = getUserRole(adminUser) // "Admin"
const guestRole = getUserRole(guestUser) // "Guest"
```

In this example:

- **`GetUserRole<T>`**: This conditional type determines the return type based on whether `T` is an `Admin` or `Guest`.
- The function **`getUserRole`** returns a different value based on the type of the user.

### 8. **Intersection and Union Types**

You can create complex types by combining multiple types using **union (`|`)** or **intersection (`&`)**.

#### Example: Union Types

```typescript
type Response =
  | { status: 'success'; data: string }
  | { status: 'error'; message: string }

function handleResponse(response: Response) {
  if (response.status === 'success') {
    console.log('Data:', response.data)
  } else {
    console.log('Error:', response.message)
  }
}
```

#### Example: Intersection Types

```typescript
type A = { a: number }
type B = { b: string }
type C = A & B // { a: number, b: string }

const obj: C = { a: 1, b: 'hello' }
```

### Summary:

- **Generics** are the foundation for creating type instances of other types.
- **Mapped Types** allow you to transform the properties of another type.
- **Conditional Types** allow for dynamic type selection based on conditions.
- **Utility Types** provide tools for creating more complex types based on existing types.
- **Union** and **Intersection Types** combine multiple types to handle complex type scenarios.
