---
layout: post
title: What do you need to know about hoisting?!
description: >
  "The term 'hoisting' describes the behavior of moving declarations to the top." - MDN
image: /assets/img/blog/javascript/july_2025/javascript_hoisting.webp
sitemap: true
---

JavaScript hoisting is one of those concepts that can trip up developers at any level. You might have encountered mysterious `undefined` values or unexpected function behaviors without realizing hoisting was the culprit. Let's demystify this fundamental JavaScript behavior.

* this ordered seed list will be replaced by the toc
{:toc}

## What is Hoisting?

As the MDN documentation states: *"The term 'hoisting' describes the behavior of moving declarations to the top."* But what does this actually mean in practice?

Hoisting is JavaScript's default behavior of moving variable and function declarations to the top of their containing scope during the compilation phase, before code execution begins. This means you can use variables and functions before they appear to be declared in your code.

## Variable Hoisting: The Three Flavors

### `var` Hoisting

Variables declared with `var` are hoisted to the top of their function scope (or global scope if declared outside a function).

```javascript
// What you write:
console.log(myVar); // undefined (not ReferenceError!)
var myVar = 5;
console.log(myVar); // 5

// How JavaScript interprets it:
var myVar; // Declaration hoisted
console.log(myVar); // undefined
myVar = 5; // Assignment stays in place
console.log(myVar); // 5
```

**Key insight**: Only the declaration is hoisted, not the initialization. The variable exists but has the value `undefined` until the assignment is reached.

### `let` and `const` Hoisting

Here's where it gets interesting. `let` and `const` are technically hoisted, but they behave very differently:

```javascript
// This throws a ReferenceError
console.log(myLet); // ReferenceError: Cannot access 'myLet' before initialization
let myLet = 10;

// Same with const
console.log(myConst); // ReferenceError: Cannot access 'myConst' before initialization
const myConst = 20;
```

This happens because of the **Temporal Dead Zone (TDZ)** - the period between the start of the scope and the actual declaration where the variable cannot be accessed.

## Function Hoisting: Declarations vs Expressions

### Function Declarations

Function declarations are fully hoisted - both the name and the function body:

```javascript
// This works perfectly
sayHello(); // "Hello, World!"

function sayHello() {
  console.log("Hello, World!");
}
```

### Function Expressions

Function expressions follow variable hoisting rules:

```javascript
// This throws an error
sayGoodbye(); // TypeError: sayGoodbye is not a function

var sayGoodbye = function() {
  console.log("Goodbye!");
};

// How JavaScript sees it:
var sayGoodbye; // undefined
sayGoodbye(); // TypeError: undefined is not a function
sayGoodbye = function() {
  console.log("Goodbye!");
};
```

### Arrow Functions

Arrow functions behave like function expressions:

```javascript
// This won't work
greet(); // ReferenceError: Cannot access 'greet' before initialization

const greet = () => {
  console.log("Hi there!");
};
```

## Import Statement Hoisting

ES6 import statements are hoisted and processed before any other code:

```javascript
// This works even though import comes after
myModule.doSomething(); // Works!

import * as myModule from './my-module.js';
```

This is why imports are always processed first, regardless of where they appear in your file.

## Real-World Examples and Gotchas

### The Classic Interview Question

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => {
    console.log(i); // Prints 3, 3, 3 (not 0, 1, 2)
  }, 100);
}

// Why? Because var is function-scoped, not block-scoped
// All setTimeout callbacks reference the same 'i' variable
```

**Solution with `let`:**

```javascript
for (let i = 0; i < 3; i++) {
  setTimeout(() => {
    console.log(i); // Prints 0, 1, 2
  }, 100);
}
```

### Function Declaration vs Expression Gotcha

```javascript
// This works
if (true) {
  function foo() {
    return "declaration";
  }
}

// But this behavior is inconsistent across environments
// Better to use function expressions in blocks:
if (true) {
  const foo = function() {
    return "expression";
  };
}
```

### Class Hoisting Behavior

Classes are hoisted but remain in the Temporal Dead Zone:

```javascript
// This throws ReferenceError
const instance = new MyClass(); // ReferenceError

class MyClass {
  constructor() {
    this.name = "example";
  }
}
```

## Strict Mode Differences

In strict mode, some hoisting behaviors change:

```javascript
"use strict";

// This throws ReferenceError in strict mode
console.log(undeclaredVar); // ReferenceError
undeclaredVar = 5; // This would create a global in non-strict mode
```

## Best Practices to Avoid Hoisting Pitfalls

### 1. Declare Variables at the Top

```javascript
// Good practice
function processData() {
  var result;
  var temp;
  var index;
  
  // ... rest of function logic
}
```

### 2. Use `const` and `let` Instead of `var`

```javascript
// Prefer this
const API_URL = "https://api.example.com";
let userCount = 0;

// Over this
var API_URL = "https://api.example.com";
var userCount = 0;
```

### 3. Initialize Variables When Declaring

```javascript
// Good
let items = [];
let isLoading = false;

// Avoid
let items;
let isLoading;
// ... later in code
items = [];
isLoading = false;
```

### 4. Use Function Expressions for Conditional Functions

```javascript
// Instead of this (inconsistent behavior)
if (condition) {
  function helper() { /* ... */ }
}

// Do this
let helper;
if (condition) {
  helper = function() { /* ... */ };
}
```

### 5. Understand the Temporal Dead Zone

```javascript
// This helps catch errors early
function processUser(user) {
  // Don't access userName here - it's in TDZ
  
  if (user) {
    let userName = user.name; // Declaration and initialization
    return userName.toUpperCase();
  }
  
  return "Anonymous";
}
```

## Debugging Hoisting Issues

When debugging hoisting-related problems:

1. **Check for `undefined` vs `ReferenceError`**:
   - `undefined`: Variable is hoisted but not initialized
   - `ReferenceError`: Variable is in TDZ or not declared

2. **Use your browser's debugger**:
   - Set breakpoints to see variable states
   - Check the scope panel to see hoisted variables

3. **Enable strict mode**:
   - Catches more hoisting-related errors
   - Prevents accidental global variable creation

## Conclusion

Hoisting is a fundamental JavaScript concept that affects how your code executes. While it can seem magical or confusing at first, understanding these rules will help you:

- Write more predictable code
- Debug issues faster
- Avoid common pitfalls in interviews and production code
- Make better decisions about variable and function declarations

Remember: modern JavaScript practices with `const`, `let`, and proper code organization can help you avoid most hoisting-related issues. When in doubt, declare your variables at the top of their scope and initialize them immediately.

The key is not to fight hoisting, but to understand it and write code that works with JavaScript's natural behavior rather than against it.
