![bg](riki-and-dan.jpg)

---

# Local First Apps

---

# Notion

- requires connection
- data stored on their servers
- offline mode is most requested feature
- they promise it...
- ...but will **never** implement it

---

# Apple

- almost all their apps are local-first
- they keep their users **hostage** in different ways

---

# Local First Apps

[inkandswitch.com/local-first](https://www.inkandswitch.com/local-first/)

- all data is **local**
- changes are **immediate** (no spinners!)
- sync is **eventual**

---

# Sync

- eventual
- on background
- **if and when** network connection is available
- connection speed quality does not matter

---

# Automerge

[github.com/automerge](https://github.com/automerge/automerge)

---
# Automerge
## Creating data

```javascript
let localDoc = Automerge.init()
localDoc = Automerge.change(localDoc, 'Add todo items', (doc) => {
  doc.todo = []
  doc.todo.push({title: 'Do something', done: false})
  doc.todo.push({title: 'Do something else', done: false})
})
```
---
# Automerge
## Merging data

```javascript
localDoc = Automerge.change(localDoc, 'Mark item as done', (doc) => {
  doc.todo[0].done = true
})
onlineDoc = Automerge.change(onlineDoc, 'Delete item', (doc) => {
  delete doc.todo[1]
})

localDoc = Automerge.merge(localDoc, offlineDoc)
```
---
# Automerge
## Managing conflicts

```javascript
localDoc = Automerge.change(localDoc, 'Rename item', (doc) => {
  doc.todo[0].title = 'This is done'
})
onlineDoc = Automerge.change(onlineDoc, 'Rename item', (doc) => {
  doc.todo[0].title = 'This is definitely not done'
})

let mergedDoc = Automerge.merge(localDoc, offlineDoc)
let conflicts = Automerge.getConflicts(mergedDoc.todo[0], 'title')
// ['This is done', 'This is definitely not done']
```
---

# Data Consistency

## Strong Consistency

- limited application logic
- high latency

## Eventual Consistency

- high availability
- low latency for write operations
- may lead to inconsistencies and data loss on conflicts

---

# Data Consistency

## Strong eventual consistency

- high availability, low latency
- ensures convergence without conflicts
- limited data types

---

# CRDT

## Conflict-free Replicated Data Types

[medium.com/@amberovsky/crdt-conflict-free-replicated-data-types](https://medium.com/@amberovsky/crdt-conflict-free-replicated-data-types-b4bfc8459d26)

---

# SQLite in browser

[sql.js.org](https://sql.js.org/)

- compiled to WASM
- uses OPFS

---

# Origin Private File System

- [fs.spec.whatwg.org/#origin-private-file-system](https://fs.spec.whatwg.org/#origin-private-file-system)
- [developer.mozilla.org/en-US/docs/Web/API/File_System_Access_API](https://developer.mozilla.org/en-US/docs/Web/API/File_System_Access_API#origin_private_file_system)
- [developer.chrome.com/articles/origin-private-file-system/](https://developer.chrome.com/articles/origin-private-file-system/)

---

# OPFS Explorer

- Chrome Extension
- [chrome.google.com/webstore/detail/opfs-explorer/acndjpgkpaclldomagafnognkcgjignd](https://chrome.google.com/webstore/detail/opfs-explorer/acndjpgkpaclldomagafnognkcgjignd)

---

# Evolu

## Technologies

- [SQLite](https://sql.js.org/)
- [NextJS](https://nextjs.org/)
- [@Effect](https://github.com/Effect-TS/effect)

## Resources

- [evolu.dev](https://www.evolu.dev/)
- [Dan Steigerwald's talk at Webexpo](https://slideslive.com/39000538/why-localfirst-software-fixes-everything)
