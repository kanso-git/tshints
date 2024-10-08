Ah, I see! You’re referring to **native JavaScript objects** that come with built-in methods in TypeScript (and JavaScript) for performing various operations like iterating over keys, transforming entries, etc. Here's a breakdown of the most common ones:

### 1. **`Object` Methods**

These methods are available on all objects in JavaScript and TypeScript.

#### **`Object.keys()`**

Returns an array of the object's own enumerable property names (keys).

```typescript
const obj = { a: 1, b: 2, c: 3 }
const keys = Object.keys(obj)
console.log(keys) // ["a", "b", "c"]
```

#### **`Object.values()`**

Returns an array of the object's own enumerable property values.

```typescript
const values = Object.values(obj)
console.log(values) // [1, 2, 3]
```

#### **`Object.entries()`**

Returns an array of the object's own enumerable property `[key, value]` pairs.

```typescript
const entries = Object.entries(obj)
console.log(entries) // [["a", 1], ["b", 2], ["c", 3]]
```

#### **`Object.fromEntries()`**

Converts an array of key-value pairs (like the one returned from `Object.entries()`) back into an object.

```typescript
const entriesArray = [
  ['a', 1],
  ['b', 2],
  ['c', 3],
]
const newObj = Object.fromEntries(entriesArray)
console.log(newObj) // { a: 1, b: 2, c: 3 }
```

#### **`Object.hasOwnProperty()`**

Checks if an object has a property as its own (not inherited) property.

```typescript
console.log(obj.hasOwnProperty('a')) // true
console.log(obj.hasOwnProperty('z')) // false
```

#### **`Object.assign()`**

Copies the values of all enumerable properties from one or more source objects to a target object.

```typescript
const target = { a: 1 }
const source = { b: 2, c: 3 }
Object.assign(target, source)
console.log(target) // { a: 1, b: 2, c: 3 }
```

#### **`Object.freeze()`**

Prevents modification of existing properties in an object.

```typescript
const frozenObj = Object.freeze({ a: 1 })
// frozenObj.a = 2; // Error in strict mode
```

#### **`Object.seal()`**

Prevents new properties from being added to an object but allows existing properties to be modified.

```typescript
const sealedObj = Object.seal({ a: 1 })
sealedObj.a = 2 // Allowed
// sealedObj.b = 3; // Error
```

### 2. **`Array` Methods for Objects**

Sometimes you treat objects similarly to arrays, using functions like `forEach` to iterate over keys or values by converting objects to arrays first (e.g., using `Object.keys()` or `Object.entries()`).

#### **`forEach()`**

Iterates over an array or the keys/values of an object. To use this on an object, you’ll need to convert the object into an array of keys, values, or entries.

```typescript
Object.keys(obj).forEach((key) => {
  console.log(key, obj[key])
})
// Output: "a" 1, "b" 2, "c" 3
```

#### **`map()`**

Similar to `forEach`, but returns a new array based on the results of the callback.

```typescript
const mapped = Object.entries(obj).map(([key, value]) => `${key}: ${value}`)
console.log(mapped) // ["a: 1", "b: 2", "c: 3"]
```

#### **`filter()`**

Filters the entries of an object by a condition, usually after converting to `Object.entries()`.

```typescript
const filtered = Object.entries(obj).filter(([key, value]) => value > 1)
console.log(filtered) // [["b", 2], ["c", 3]]
```

#### **`reduce()`**

Reduces the array to a single value, often useful for summing up values or transforming an object.

```typescript
const sum = Object.values(obj).reduce((acc, val) => acc + val, 0)
console.log(sum) // 6
```

### 3. **`for...in` Loop**

Used for iterating over the enumerable properties (both own and inherited) of an object.

```typescript
for (const key in obj) {
  if (obj.hasOwnProperty(key)) {
    console.log(key, obj[key])
  }
}
// Output: "a" 1, "b" 2, "c" 3
```

### 4. **`for...of` Loop** (with `Object.entries()`)

You can use `for...of` to iterate over arrays or iterable objects like `Object.entries()`.

```typescript
for (const [key, value] of Object.entries(obj)) {
  console.log(key, value)
}
// Output: "a" 1, "b" 2, "c" 3
```

### Summary of Common Object Methods:

- **`Object.keys()`** – Get an array of property names (keys).
- **`Object.values()`** – Get an array of property values.
- **`Object.entries()`** – Get an array of `[key, value]` pairs.
- **`Object.fromEntries()`** – Convert key-value pairs back to an object.
- **`Object.hasOwnProperty()`** – Check if a property exists directly on the object.
- **`Object.assign()`** – Copy properties from one object to another.
- **`Object.freeze()`** – Make an object immutable.
- **`Object.seal()`** – Prevent adding new properties but allow modifying existing ones.

With these methods, you can manipulate and iterate over objects effectively in TypeScript!
