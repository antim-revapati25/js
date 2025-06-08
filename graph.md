# 🧮 Undirected Graph using Adjacency Matrix (JavaScript)

This script implements an undirected graph using an adjacency matrix in JavaScript.

---

## 📌 Description

- The graph is undirected, meaning each edge connects two nodes in both directions.
- The matrix is a `vertices x vertices` grid, where each cell `(i, j)` is `1` if there's an edge between node `i` and node `j`.

---

## 🧾 Code

```javascript
//implementing undirected graph using adjacency matrix
console.log("undirected graph is here...!");

// format: [0 is connected to 1], [1 is connected to 2], and so on...
const vertices = 4; // 0-based vertex names
const edges = [
  [0, 1],
  [1, 2],
  [2, 3],
  [0, 2],
];

// -----------------logic
// --> create matrix vertices * vertices
const matrix = [];
for (let i = 0; i < vertices; i++) {
  matrix.push(Array(vertices).fill(0));
}

let ind = 0;
// 0 indexed
for (let i = 0; i < edges.length; i++) {
  let data = edges[i];
  let row = data[0];
  let col = data[1];

  matrix[row][col] = 1;
  matrix[col][row] = 1;
}

console.log("\n");

for (let i = 0; i < vertices; i++) {
  console.log(matrix[i].toString() + " : " + i);
}
