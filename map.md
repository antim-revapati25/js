
# 📘 JavaScript `map()` Method – Explained

## 🔹 What is `map()`?

The `map()` method is used to **create a new array** by applying a callback function to each element of the original array. It **does not modify** the original array.

---

## 🧠 Syntax

```js
array.map(callbackFunction, thisArg)
```

### ✅ Callback Function Parameters:

1. `value` (required): Current element being processed.
2. `index` (optional): Index of the current element.
3. `array` (optional): The original array being mapped.

### ✅ Notes:

- `map()` always returns a new array.
- The **original array remains unchanged**.
- The callback function **must return** a value — otherwise, the result will be `undefined`.

---

## 📌 Example 1 – Basic Usage

```js
const arr = [10, 20, 30];

const ans = arr.map((val, ind, ar) => {
  return val + 5;
});

console.log(ans); // Output: [15, 25, 35]
```

---

## 🔍 Example 2 – Using `thisArg` with Objects and Functions

The `thisArg` is used to bind `this` to the map method. now `this` is pointing to that binding, `this` refers to the object passed as `thisArg`.

### ✅ Correct Way – Using Object as `thisArg` --> use normal function not arrow function

```js

const brr = [10, 20, 30];
const obj = {
  factor: 5,
};

const anss = brr.map(function (val, ind, arr) {
  return val + this.factor;
}, obj);

console.log(anss); // Output: [15, 25, 35]
```

---

### ❌ Incorrect Way – Using Arrow Function with `thisArg`

```js
const brr = [10, 20, 30];

const obj = {
  factor: 5,
};

const bns = brr.map((val, ind, ar) => {
  return val + this.factor; // 'this' won't refer to `obj`
}, obj);

console.log(bns); // Output: [NaN, NaN, NaN]
```

> ❗ Why this fails:
> Arrow functions **do not have their own `this`**. They inherit `this` from their lexical scope (usually `window` in non-strict mode and `undefined` in strict mode), so passing `thisArg` has no effect.

---

### ⚠️ Misuse Example – Trying to Use Function as `thisArg`

```js
const brr = [10, 20, 30];

/*
Note: You can't use a function directly without calling it, because functions
do not have inbuilt `this` binding. It depends on how the function is invoked.
*/

const fun = function () {
  this.fact = 5;
};

const answer = brr.map(function (val, ind, arr) {
  return val + this.factor;
}, fun);

console.log(answer); // Output: [NaN, NaN, NaN]
```

> ❗ Since the function is not called (like `fun()` or `new fun()`), the `this` binding is never established.

---

## 💡 Why the above fails and how `this` works in JavaScript

A function’s internal `this` is `undefined` (in strict mode) or `window` (in non-strict mode) unless:

- It is called normally (e.g., `fun()` → `this` is `window` or `undefined`).
- It is called with `new` (e.g., `new fun()` → `this` is a new object).
- It is called with `.call()`, `.apply()`, or `.bind()` (you manually set `this`).

---

## 🛠️ If you want to use a function, here's how:

```js
function myFun() {} // creates the function

myFun.fact = 10; // add a property to the function object
```

> ✅ In JavaScript, functions are **first-class objects**. You don’t need to call a function to assign or access its properties. Now `myFun` holds a property like an object. If passed as `thisArg`, its properties are accessible via  `this` in a regular function.

---


## 🔁 Analogy: Function vs Object Property Assignment

```js
const obj = {};
obj.factor = 10;
console.log(obj.factor); // 10
```

Now replace `obj` with the function `myFunc`:

```js
function myFunc() {}
myFunc.factor = 10;
console.log(myFunc.factor); // 10
```

> ✅ Functions can have properties just like objects because they are also objects.

---

## 🔥 Full Working Example Using Function as Object

```js
function myFunc() {}
myFunc.factor = 3; // assign property to function-object

const arr = [1, 2, 3];
const result = arr.map(function (val) {
  return val * this.factor;
}, myFunc); // myFunc is used as the 'thisArg'

console.log(result); // [3, 6, 9]
```

---

## 📌 Summary

| Concept                                    | Truth                                       |
|--------------------------------------------|---------------------------------------------|
| Modifies original array                    | ❌ No                                        |
| Returns new array                          | ✅ Yes                                       |
| Requires `return`                          | ✅ Yes                                       |
| Works with `thisArg`                       | ✅ Only with regular functions or objects    |
| Arrow functions respect `thisArg`?         | ❌ No                                        |
| Are functions objects?                     | ✅ Yes                                       |
| Can functions have properties like `func.prop = 5`? | ✅ Yes                        |
| Do you need to call the function to use it as `thisArg`? | ❌ No if used as object |
| Can `thisArg` be a function?               | ✅ Yes, because it's also an object          |
| Does `this` inside function body work if function isn't called? | ❌ No             |
