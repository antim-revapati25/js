# Understanding Nested Array Reference Behavior in JavaScript

## Problem Description

When creating nested arrays using `Array.fill()`, unexpected behavior can occur where changing one element inside a nested array modifies multiple arrays. This happens due to references being shared instead of independent copies being created.

---

## Explanation

- `Array(2).fill(0)` creates a new array of length 2 filled with `0`.
- When you do `Array(3).fill(Array(2).fill(0))`, **it fills the outer array with references to the *same* inner array**.
- This means all three elements in the outer array point to the **same** inner array.
- Modifying one element in any of these inner arrays modifies that same shared array, so all appear changed.

---

## Code Example

```javascript
let arr = Array(3).fill(Array(2).fill(0));
arr[0][1] = 1;  // Modify element at index 1 of the first inner array
console.log(arr); 
```
---
## Output Explanation

The output will be:

```js
[
  [0, 1],
  [0, 1],
  [0, 1]
]
```

- Changing `arr[0][1]` to `1` changes that position in all three inner arrays because they are all references to the **same** array.  
- This behavior often surprises developers expecting each inner array to be independent.

---
