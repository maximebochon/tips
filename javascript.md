# JavaScript

## `var`, `let` and variable scope

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
