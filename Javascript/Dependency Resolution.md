## What is Dependency Resolution? 
Dependency resolution is the process of identifying and managing the modules and packages that your application requires. 

## Dependency Resolution techniques in JS ecosystem . 

### Static Linking
 **Description** : 
 The dependency tree is resolved and bundled into a single or multiple output files during the build process.
Tools like webpack rollup etc. analyze import/require statements and include dependency in the final bundle. 

**Advantages**
Optimized bundles for production.
Supports, code splitting and tree shaking. 
### Dynamic Linking
**Description** 
Dependencies are resolved at runtime and fetched as needed. 

The application uses import() for lazy or dynamic imports.
Modules are loaded asynchronoulsy.

**Advantages**
Enables on demand loading and reduces initial page load size. 


### Node.js Module resolution

**Description**
Follows Node.js module resolution algorithm . 
Resolves modules from node_modules.

### ES Module resolution

**Description** 
Uses native JS ES module standard for dependency managment.

import /export syntax is used to define and load modules.
### Pre-bundling

**Description**
Dependencies are prebundled before runtime to optimize performance.
Tools like Vite use esbuild to bundle dependencies into ESM format before running the development server. 
### CDN based resolution

**Description**
Dependencies are fetched directly from a CDN at runtime. 
LIbraries are imported via script tags or ESM imports from a CDN
### Runtime Resolution
**Description**
Dependencies are resolved dynamically during application runtime. 

Libraries like SystemJS dynamically load and resolve modules using its runtime loader. 
### Server Side Resolution
**Description**

Dependencies are resolved by a backend of middleware. 

The server provies the client with the necessary modules dynamically. 

### **Choosing the Right Technique**

- **Static Bundling:** Best for production-ready applications with advanced optimizations.
- **Dynamic Linking:** Ideal for scenarios where runtime adaptability is critical.
- **ESM:** Preferred for modern projects due to native support and optimization capabilities.
- **CDN:** Great for prototyping or small-scale projects.
### Diagram

```
+--------------------------+
| Static Linking           |
| (Webpack, Rollup, etc.)  |
+--------------------------+
          |
          v
+--------------------------+
| Dynamic Linking          |
| (import(), lazy loading) |
+--------------------------+
          |
          v
+--------------------------+
| Node.js Module Resolution|
| (require())              |
+--------------------------+
          |
          v
+--------------------------+
| ESM Resolution           |
| (import/export)          |
+--------------------------+
          |
          v
+--------------------------+
| Pre-Bundling            |
| (esbuild, Vite)         |
+--------------------------+
          |
          v
+--------------------------+
| CDN-Based Resolution     |
| (jsDelivr, Skypack)      |
+--------------------------+

```

## Vite

```
Source Code
   |
   v
[Dependency Scanner]
   |
   v
[Pre-Bundling with esbuild]
   |
   v
Optimized Modules (stored in `node_modules/.vite`)
   |
   v
[Dev Server]
   |
   v
Browser Requests Modules Dynamically

```
