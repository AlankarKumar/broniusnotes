Native ES Modules (often abbreviated as ESM) are a modern JavaScript module system introduced in **ECMAScript 2015 (ES6)**. They allow developers to organize code into reusable, maintainable, and efficient modules. Unlike earlier module systems like CommonJS or AMD, ESM is a built-in feature of JavaScript, supported natively by modern browsers and Node.js.

### **Key Features of Native ES Modules**

1. **Static Structure**
    
    - Imports and exports are statically analyzed at compile time.
    - This makes features like tree-shaking and bundling optimizations possible.
2. **`import` and `export` Syntax**
    
    - Use `import` to include modules and `export` to share parts of a module.
```
// math.js
export const add = (a, b) => a + b;

// app.js
import { add } from './math.js';
console.log(add(2, 3)); // 5

```

- **File-Based Modules**
    
    - Each file is treated as a separate module.
    - Modules are loaded relative to their location or via URLs.
- **Asynchronous Loading**
    
    - Modules are loaded asynchronously by default, meaning they do not block execution.
    - This improves performance, especially in browser environments.
- **Strict Mode**
    
    - ESM operates in strict mode by default, enforcing cleaner and less error-prone code.
- **Scoped Variables**
    
    - Variables in a module are scoped to that module and do not pollute the global scope.
- **Default Exports**
    
    - Modules can have a default export, which simplifies importing when only one main functionality is exported.
```
// utils.js
export default function greet(name) {
  return `Hello, ${name}!`;
}

// app.js
import greet from './utils.js';
console.log(greet('Alice')); // Hello, Alice!

```


## Native ESM in browsers

- Modules are fetched and executed asynchronously.
- Relative paths or absolute URLs must be specified.
- 
```
<!DOCTYPE html>
<html lang="en">
<head>
  <title>ESM Example</title>
</head>
<body>
  <script type="module">
    import { add } from './math.js';
    console.log(add(5, 7)); // 12
  </script>
</body>
</html>

```


### Native ESM in Node.js

Starting from Node.js **v12**, ESM is supported natively. To enable it:

1. Use `.mjs` file extensions, or
2. Add `"type": "module"` to `package.json`.
```

// utils.mjs
export const greet = (name) => `Hello, ${name}!`;

// main.mjs
import { greet } from './utils.mjs';
console.log(greet('Bob')); // Hello, Bob!

//dynamic import
const module = await import('./utils.mjs');
console.log(module.greet('Alice'));


```


## Bare Module imports

A **bare module import** refers to the use of a package name (e.g., `'my-dep'`) without specifying a file path or a URL. This is common in Node.js and tools like Webpack, where dependency resolution automatically looks in `node_modules`.

```
import { someMethod } from 'my-dep'; // Bare module import

```

### **Why Do Bare Module Imports Fail in Native ESM?**

Browsers dont follow nodejs module resolution algorithm.

They treat deps as literal path . 

```
import { someMethod } from 'my-dep';
// Browser tries to fetch <origin>/my-dep, leading to a 404 error.

```