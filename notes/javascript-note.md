---
title: Remove Duplicates
tags:
  - javascript
emoji: 👋
---

### Remove Duplicates

```js
const array = ["🐑", 1, 2, "🐑", "🐑", 3];

// 1: "Set"
[...new Set(array)];

// 2: "Filter"
array.filter((item, index) => array.indexOf(item) === index);

// 3: "Reduce"
array.reduce(
  (unique, item) => (unique.includes(item) ? unique : [...unique, item]),
  []
);

// RESULT:
// ['🐑', 1, 2, 3];
```
