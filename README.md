# Browser IndexedDB Client Storage Architecture

> A practical case study demonstrating how IndexedDB enables scalable, transactional and offline-first storage in modern web applications.

![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-yellow?style=for-the-badge&logo=javascript)
![IndexedDB](https://img.shields.io/badge/Storage-IndexedDB-blue?style=for-the-badge)
![Browser](https://img.shields.io/badge/Environment-Browser-green?style=for-the-badge&logo=googlechrome)
![Architecture](https://img.shields.io/badge/Focus-Client%20Side%20Architecture-purple?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Case%20Study-black?style=for-the-badge)

---

## Overview

IndexedDB is a low-level browser API that enables applications to store large volumes of structured data on the client side.

Unlike LocalStorage, IndexedDB supports:

- Transactions
- Indexes
- Complex queries
- Large data storage
- Binary data (files, blobs)

This makes it ideal for modern applications that require offline capabilities and high performance.

---

## The Problem

Traditional browser storage solutions are limited:

```text
LocalStorage:
- Small capacity (~5MB)
- Synchronous (blocks UI)
- No indexing
- No transactions
```
Modern applications require:
```text
Offline support
Fast reads
Large datasets
Efficient querying
```
## What is IndexedDB?

IndexedDB is a transactional database inside the browser.
```text
Browser → IndexedDB → Object Stores → Indexed Data
```
It allows applications to:

Store structured objects
Query using indexes
Handle large datasets
Work offline

## Architecture
```text
User Interface
      ↓
Application Logic (JavaScript)
      ↓
IndexedDB API
      ↓
Object Store (tables)
      ↓
Indexed Data
```

## Key Concepts
Object Store

Equivalent to a table:
```js
db.createObjectStore("clientes", { keyPath: "id" });
```
## Indexes

Allow fast queries:
```js
store.createIndex("email", "email", { unique: true });
```
## Transactions

Ensure consistency:
```js
const transaction = db.transaction(["clientes"], "readwrite");
```
## Example
Opening Database
```js
const request = indexedDB.open("MinhaBase", 1);

request.onupgradeneeded = function (event) {
  const db = event.target.result;

  const store = db.createObjectStore("clientes", { keyPath: "id" });
  store.createIndex("email", "email", { unique: true });
};
```
## Inserting Data
```js
const transaction = db.transaction(["clientes"], "readwrite");
const store = transaction.objectStore("clientes");

store.add({
  id: 1,
  nome: "Thiago",
  email: "thiago@email.com"
});
```
## Query by Index
```js
const index = store.index("email");
const request = index.get("thiago@email.com");

request.onsuccess = () => {
  console.log(request.result);
};
```

## IndexedDB vs LocalStorage

| Feature | IndexedDB | LocalStorage |
| :--- | :--- | :--- |
| **Capacity** | Large | Small |
| **Async** | Yes | No |
| **Transactions** | Yes | No |
| **Indexing** | Yes | No |
| **Data type** | Objects | Strings |

## When to Use IndexedDB

Use IndexedDB when:

You need offline-first applications
You handle large datasets
You need complex queries
You need structured storage
You want better performance than LocalStorage

## Real Engineering Use Cases

Offline-first mobile apps (PWA)
Caching API responses locally
Form data persistence
Large client-side datasets
Sync systems (client ↔ server)

## Demo
## Layout API Indexed DB ![Mobile 1](https://github.com/Thiago771414/imagensProjetos/blob/main/slices/mobile/IndexedDB.png) 
## Vídeo de demonstração [[Vídeo de demonstração]](https://youtu.be/ukLVApnLPqg)

## Architecture Insight
```text
Server = source of truth
IndexedDB = local performance layer
API = synchronization bridge
```
## Common Mistakes

❌ Using LocalStorage for large data
❌ Ignoring transactions
❌ Not using indexes
❌ Treating IndexedDB like a simple key-value store
❌ Not handling version upgrades

## Summary

IndexedDB is not just storage.

It is a client-side database engine.
```text
LocalStorage = simple cache
IndexedDB = structured database
```
```markdown
## Advanced Topics

- Offline-first architecture
- Sync strategies (client ↔ server)
- Conflict resolution
- IndexedDB + Service Workers
```
## Author

Thiago Lima
Software Engineer | System Design | Frontend Architecture
