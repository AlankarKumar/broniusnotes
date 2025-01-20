**Description**

**Hot Module Replacement (HMR)** is a development feature that enables a web application to update modules in the browser without requiring a full page reload. It is commonly used in modern frontend development tools like Vite, Webpack, and Parcel.

### **How Does HMR Work?**

1. **Dependency Graph Tracking**:  
    The development server keeps track of the dependency graph of your modules. When a file changes, the server determines which modules are affected.
    
2. **Push Updates**:  
    Instead of reloading the entire page, the development server pushes updates for only the changed modules to the browser via WebSocket.
    
3. **Update Application State**:  
    The browser applies the changes in memory, preserving the current state of the application (like UI state or form inputs).
    
4. **Module-Specific Handlers**:  
    Modules can define how they handle updates by implementing HMR APIs, allowing for custom logic during module replacement.


**Diagram: HMR Workflow**

```
[Source Code Changes]
         |
         v
[Dev Server Watches Changes]
         |
         v
[Modified Module Bundled]
         |
         v
[WebSocket Push Update]
         |
         v
[HMR Runtime Applies Update]
         |
         v
[UI Reflects Changes Without Reloading]

```