---
layout: post
title: Javascript closure
description: >
  "A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment)." - MDN
image: /assets/img/blog/javascript/july_2025/javascript-closure.webp
sitemap: true
category: javascript
tags:
- javascript
---

JavaScript closures are one of the most powerful and fundamental concepts in the language, yet they often mystify developers. You've likely used closures without even realizing it! Understanding closures will unlock advanced patterns and help you write more elegant, maintainable code.

* this ordered seed list will be replaced by the toc
{:toc}

## What are Closures?

According to MDN: *"A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment)."*

In simpler terms, a closure gives you access to an outer function's scope from an inner function. The inner function has access to variables in three scopes:
- Its own scope (variables defined between its curly brackets)
- The outer function's variables
- Global variables

## Simple Explanation: The Box Analogy

Before we dive into the technical details, let's understand closures with a simple analogy that makes the concept crystal clear.

As explained by @mukeshb on DevTo: *"Imagine you have a box (a function) with some items inside it (variables). So, once you close the box, you cannot access the items inside from the outside. However, with closure, you have a magical way of reaching into the box and using those items even after the box is closed."*

Let's expand on this analogy:

Think of a function as a **box** that contains **items** (variables). Normally, when you close the box (the function finishes executing), those items become inaccessible from the outside world. But closures give you a **magical key** - a way to reach back into that closed box and use those items whenever you need them.

Here's how this looks in actual JavaScript:

```javascript
function createBox(item) {
  // This is our "box" with an "item" inside
  let treasureInside = `You found: ${item}`;
  
  // This is our "magical key" - a function that can reach into the closed box
  function openBox() {
    return treasureInside; // We can still access the item!
  }
  
  return openBox; // We give you the magical key
}

// Create a box and get the magical key
const magicalKey = createBox("a golden coin");

// The box (createBox function) has finished executing and is "closed"
// But we can still access what's inside using our magical key!
console.log(magicalKey()); // "You found: a golden coin"

// Even after the original function is done, the treasure is still accessible
setTimeout(() => {
  console.log(magicalKey()); // Still works! "You found: a golden coin"
}, 1000);
```

**What's happening here?**
1. The `createBox` function is our "box" containing the `treasureInside` variable
2. When `createBox` finishes executing, it's "closed" - normally, `treasureInside` would be gone
3. But the `openBox` function acts as our "magical key" - it remembers and can access `treasureInside`
4. This magical connection between the inner function and the outer function's variables is what we call a **closure**

This is the essence of closures: inner functions maintaining access to outer function variables even after the outer function has completed execution. It's like having a permanent, magical connection to variables that should theoretically be out of reach.

## Understanding Lexical Scoping

Before diving into closures, let's understand lexical scoping - the foundation upon which closures are built:

```javascript
function outerFunction(x) {
  // This is the outer function's scope
  
  function innerFunction(y) {
    // This inner function has access to the outer function's variables
    console.log(x + y); // x is accessible here!
  }
  
  return innerFunction;
}

const myFunction = outerFunction(10);
myFunction(5); // Prints: 15
```

The `innerFunction` can access the `x` parameter from `outerFunction` even after `outerFunction` has finished executing. This is a closure in action!

## Basic Closure Examples

### Example 1: Simple Closure

```javascript
function createGreeting(name) {
  return function(message) {
    console.log(`${message}, ${name}!`);
  };
}

const greetJohn = createGreeting("John");
greetJohn("Hello"); // "Hello, John!"
greetJohn("Good morning"); // "Good morning, John!"

// The 'name' variable is still accessible even though
// createGreeting has finished executing
```

### Example 2: Counter Function

```javascript
function createCounter() {
  let count = 0; // Private variable
  
  return function() {
    count++; // Accessing and modifying the outer variable
    return count;
  };
}

const counter1 = createCounter();
const counter2 = createCounter();

console.log(counter1()); // 1
console.log(counter1()); // 2
console.log(counter2()); // 1 (independent counter)
console.log(counter1()); // 3
```

**Key insight**: Each call to `createCounter()` creates a new closure with its own `count` variable. The counters are completely independent!

## Data Privacy with Closures

Closures provide a way to create private variables in JavaScript:

```javascript
function createBankAccount(initialBalance) {
  let balance = initialBalance; // Private variable
  
  return {
    deposit: function(amount) {
      if (amount > 0) {
        balance += amount;
        return balance;
      }
      throw new Error("Deposit amount must be positive");
    },
    
    withdraw: function(amount) {
      if (amount > 0 && amount <= balance) {
        balance -= amount;
        return balance;
      }
      throw new Error("Invalid withdrawal amount");
    },
    
    getBalance: function() {
      return balance;
    }
  };
}

const account = createBankAccount(100);
console.log(account.getBalance()); // 100
account.deposit(50);
console.log(account.getBalance()); // 150

// balance is not directly accessible
console.log(account.balance); // undefined
```

## Module Pattern with Closures

Closures enable the module pattern, creating encapsulated modules with public and private methods:

```javascript
const Calculator = (function() {
  // Private variables and functions
  let history = [];
  
  function addToHistory(operation, result) {
    history.push(`${operation} = ${result}`);
  }
  
  // Public API
  return {
    add: function(a, b) {
      const result = a + b;
      addToHistory(`${a} + ${b}`, result);
      return result;
    },
    
    multiply: function(a, b) {
      const result = a * b;
      addToHistory(`${a} * ${b}`, result);
      return result;
    },
    
    getHistory: function() {
      return [...history]; // Return a copy
    },
    
    clearHistory: function() {
      history = [];
    }
  };
})();

console.log(Calculator.add(5, 3)); // 8
console.log(Calculator.multiply(4, 2)); // 8
console.log(Calculator.getHistory()); // ["5 + 3 = 8", "4 * 2 = 8"]
```

## Event Handlers and Callbacks

Closures are commonly used in event handlers and callbacks:

```javascript
function setupButton(name) {
  return function(event) {
    console.log(`Button ${name} was clicked!`);
    console.log('Event details:', event.type);
  };
}

// In a real application:
// document.getElementById('btn1').addEventListener('click', setupButton('Save'));
// document.getElementById('btn2').addEventListener('click', setupButton('Cancel'));

// Each button gets its own closure with the specific name
```

### Practical Example: Dynamic Event Handlers

```javascript
function createClickHandlers() {
  const buttons = ['Home', 'About', 'Contact'];
  const handlers = [];
  
  for (let i = 0; i < buttons.length; i++) {
    handlers.push(function() {
      console.log(`Navigating to ${buttons[i]} page`);
    });
  }
  
  return handlers;
}

const handlers = createClickHandlers();
handlers[0](); // "Navigating to Home page"
handlers[1](); // "Navigating to About page"
```

## Advanced Use Cases

### Function Factories

```javascript
function createMultiplier(multiplier) {
  return function(number) {
    return number * multiplier;
  };
}

const double = createMultiplier(2);
const triple = createMultiplier(3);

console.log(double(5)); // 10
console.log(triple(5)); // 15
```

### Memoization with Closures

```javascript
function memoize(fn) {
  const cache = {};
  
  return function(...args) {
    const key = JSON.stringify(args);
    
    if (cache[key]) {
      console.log('Cache hit!');
      return cache[key];
    }
    
    console.log('Computing result...');
    const result = fn.apply(this, args);
    cache[key] = result;
    return result;
  };
}

const expensiveFunction = memoize(function(n) {
  // Simulate expensive computation
  let result = 0;
  for (let i = 0; i < n * 1000000; i++) {
    result += i;
  }
  return result;
});

console.log(expensiveFunction(100)); // Computing result... (takes time)
console.log(expensiveFunction(100)); // Cache hit! (instant)
```

### Partial Application

```javascript
function partial(fn, ...presetArgs) {
  return function(...laterArgs) {
    return fn(...presetArgs, ...laterArgs);
  };
}

function greet(greeting, punctuation, name) {
  return `${greeting}, ${name}${punctuation}`;
}

const sayHello = partial(greet, "Hello", "!");
const sayGoodbye = partial(greet, "Goodbye", ".");

console.log(sayHello("Alice")); // "Hello, Alice!"
console.log(sayGoodbye("Bob")); // "Goodbye, Bob."
```

## Common Pitfalls and Edge Cases

### The Classic Loop Problem

```javascript
// Problem: All buttons alert "3"
function createButtons() {
  for (var i = 0; i < 3; i++) {
    setTimeout(function() {
      console.log(`Button ${i} clicked`); // Always prints "Button 3 clicked"
    }, 100);
  }
}

// Solution 1: Use let instead of var
function createButtonsFixed1() {
  for (let i = 0; i < 3; i++) {
    setTimeout(function() {
      console.log(`Button ${i} clicked`); // Prints 0, 1, 2
    }, 100);
  }
}

// Solution 2: Create a closure with IIFE
function createButtonsFixed2() {
  for (var i = 0; i < 3; i++) {
    (function(index) {
      setTimeout(function() {
        console.log(`Button ${index} clicked`); // Prints 0, 1, 2
      }, 100);
    })(i);
  }
}
```

### Memory Leaks and Garbage Collection

```javascript
// Potential memory leak
function problematicClosure() {
  const largeData = new Array(1000000).fill('data');
  
  return function() {
    // Even though we don't use largeData,
    // it's kept in memory because of the closure
    console.log('Function called');
  };
}

// Better approach: only capture what you need
function betterClosure() {
  const largeData = new Array(1000000).fill('data');
  const summary = `Data length: ${largeData.length}`;
  
  return function() {
    console.log(summary); // Only captures summary, not largeData
  };
}
```

### Debugging Closure Issues

```javascript
function debugClosure() {
  let secretValue = 42;
  
  function innerFunction() {
    console.log('Secret value:', secretValue);
    // Use debugger to inspect closure scope
    debugger;
  }
  
  return innerFunction;
}

const debugFn = debugClosure();
debugFn(); // Open browser dev tools to see closure scope
```

## Performance Considerations

### When Closures Might Impact Performance

```javascript
// Inefficient: Creates new function on every call
function inefficientHandler(data) {
  return data.map(function(item) {
    return function() {
      console.log(item);
    };
  });
}

// More efficient: Reuse function when possible
function efficientHandler(data) {
  function logItem(item) {
    return function() {
      console.log(item);
    };
  }
  
  return data.map(logItem);
}
```

## Best Practices

### 1. Use Closures for Data Privacy

```javascript
// Good: Encapsulate state
function createTimer() {
  let startTime = Date.now();
  
  return {
    getElapsed: () => Date.now() - startTime,
    reset: () => startTime = Date.now()
  };
}
```

### 2. Avoid Unnecessary Closures

```javascript
// Avoid: Unnecessary closure
function unnecessary() {
  return function(x) {
    return x * 2;
  };
}

// Better: Direct function
function double(x) {
  return x * 2;
}
```

### 3. Be Mindful of Memory Usage

```javascript
// Good: Clean up references when done
function createHandler() {
  let cache = new Map();
  
  const handler = function(data) {
    // Use cache
  };
  
  handler.cleanup = function() {
    cache.clear();
    cache = null;
  };
  
  return handler;
}
```

### 4. Use Modern Syntax When Appropriate

```javascript
// Modern approach with arrow functions
const createMultiplier = (factor) => (number) => number * factor;

// Class-based approach for complex state
class Counter {
  #count = 0; // Private field
  
  increment() {
    return ++this.#count;
  }
  
  getCount() {
    return this.#count;
  }
}
```

## Real-World Applications

### API Client with Closure-Based Configuration

```javascript
function createApiClient(baseUrl, apiKey) {
  const defaultHeaders = {
    'Authorization': `Bearer ${apiKey}`,
    'Content-Type': 'application/json'
  };
  
  return {
    get: async function(endpoint) {
      const response = await fetch(`${baseUrl}${endpoint}`, {
        headers: defaultHeaders
      });
      return response.json();
    },
    
    post: async function(endpoint, data) {
      const response = await fetch(`${baseUrl}${endpoint}`, {
        method: 'POST',
        headers: defaultHeaders,
        body: JSON.stringify(data)
      });
      return response.json();
    }
  };
}

const api = createApiClient('https://api.example.com', 'your-api-key');
// api.get('/users') automatically includes auth headers
```

## Conclusion

Closures are a fundamental JavaScript concept that enables:

- **Data privacy** and encapsulation
- **Function factories** and specialized functions
- **Module patterns** for organizing code
- **Event handling** with context preservation
- **Advanced patterns** like memoization and partial application

Understanding closures will help you:
- Write more maintainable and organized code
- Implement advanced design patterns
- Debug scope-related issues more effectively
- Appreciate how many JavaScript features work under the hood

Remember: closures are created every time a function is created. They're not just an advanced feature - they're a core part of how JavaScript works. Master them, and you'll have a powerful tool for writing elegant, efficient code.

The key is to use closures purposefully, understanding both their power and their potential pitfalls. When used correctly, they make JavaScript code more expressive and maintainable.