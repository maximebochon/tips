# JavaScript

## `var`, `let`, `const` and variable scope

The `var` keyword defines *function scoped* variables.
Indeed, in traditional JavaScript, `{` does not create a new *variable scope*:

```ts
var x = 10;

if (true) {
    var x = 20;
}

console.log(x); // 20
```

The `let` keyword introduced in TypeScript and JavaScript ES6 defines *block scoped* variables:

```ts
let x = 10;

if (true) {
    let x = 20;
}

console.log(x); // 10
```

The `const` keyword defines *block scoped* constants. Their value is immutable after creation. However in the case of an object constant, it does not prevent mutating properties of this object.

```ts
const x = 10;
x = 20; // ERROR (immutable)
```

```ts
const y = 30;

if (true) {
    const y = 40; // OK (block scope)
}
```

```ts
const z = { a: 50 };

z = { a: 60 }; // ERROR (immutable)
console.log(z); // { a: 50 }

z.a = 70; // OK
console.log(z); // { a: 70 }
```

## Easy to read (indented) JSON

```javascript
const object = { a: { x: 1, y: 2}, b: { x: 10, y: 20}, c: null };
const easyToReadJSON = JSON.stringify(object, null, 2);
console.log(easyToReadJSON);
```

```json
{
  "a": {
    "x": 1,
    "y": 2
  },
  "b": {
    "x": 10,
    "y": 20
  },
  "c": null
}
```
