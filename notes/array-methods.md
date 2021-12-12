---
title: Array Methods
tags:
  - javascript
emoji: 👋
---

### forEach

- forEach compared to the map method it doesn't return anything, so is undefined
- Arguments: item, index, list

```js
[1, 2, 3].forEach((item, index) => {
  console.log(item, index);
});
```

### map

- It iterates every item of an array and returns a new array with those items
- Arguments: item, index, list

```js
const numbers = [1, 2, 3];
const isNumDoubled = numbers.map((item) => {
  return item * 2;
});
console.log(numbers === isNumDoubled, isNumDoubled); // false, [2, 4, 6]
```

### filter

- It returns a truthy or falsy value
- Arguments: item, index, list
- Returns the items that fullfiled the condition

```js
const numbers = [1, 2, 3];
const filteredArray = numbers.filter((number) => {
  return number % 2 === 0;
});
console.lognumbers === filteredArray, filteredArray); // false, [2]
```

### reduce

- The reduce method cycles through each number in the array much like it would in a for-loop.
