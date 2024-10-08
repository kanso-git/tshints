In TypeScript, you can work with **type instances of another type** and define more **complex types** using **generics**, **mapped types**, **conditional types**, and **utility types**. These constructs allow you to create types that depend on or are based on other types.

### 1. **Type Instance of Another Type (Generics)**

Generics are the primary tool for creating types that depend on other types. You can create a type where one type is based on another type's instance.

#### Example: Creating a Wrapper Type

```typescript
type Box<T> = {
  value: T
}

const stringBox: Box<string> = { value: "Hello" }
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
  name: "Alice",
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
type IsString<T> = T extends string ? "string" : "not string"

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
type UserNameAndEmail = Pick<User, "name" | "email">

// Omit age from User
type UserWithoutAge = Omit<User, "age">
```

### 6. **Type Inference with Generics**

You can infer types dynamically when using generic functions.

#### Example: Inferring Types from Function Parameters

```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key]
}

const person = { name: "John", age: 30 }

const name = getProperty(person, "name") // string
const age = getProperty(person, "age") // number
```

- **`K extends keyof T`**: This ensures that the `key` parameter is a valid property key of `T`.
- The return type is dynamically inferred based on the type of the property accessed.

### 7. **Complex Example Combining Various Concepts**

#### Example: A Function Returning a Conditional Type

```typescript
type Admin = {
  role: "admin"
  permissions: string[]
}

type Guest = {
  role: "guest"
  visitCount: number
}

type User = Admin | Guest

type GetUserRole<T extends User> = T extends Admin ? "Admin" : "Guest"

function getUserRole<T extends User>(user: T): GetUserRole<T> {
  if (user.role === "admin") {
    return "Admin" as GetUserRole<T>
  }
  return "Guest" as GetUserRole<T>
}

const adminUser: Admin = { role: "admin", permissions: ["read", "write"] }
const guestUser: Guest = { role: "guest", visitCount: 5 }

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
  | { status: "success"; data: string }
  | { status: "error"; message: string }

function handleResponse(response: Response) {
  if (response.status === "success") {
    console.log("Data:", response.data)
  } else {
    console.log("Error:", response.message)
  }
}
```

#### Example: Intersection Types

```typescript
type A = { a: number }
type B = { b: string }
type C = A & B // { a: number, b: string }

const obj: C = { a: 1, b: "hello" }
```

### Summary:

- **Generics** are the foundation for creating type instances of other types.
- **Mapped Types** allow you to transform the properties of another type.
- **Conditional Types** allow for dynamic type selection based on conditions.
- **Utility Types** provide tools for creating more complex types based on existing types.
- **Union** and **Intersection Types** combine multiple types to handle complex type scenarios.
