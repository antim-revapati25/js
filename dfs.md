
# 🔍 Understanding Depth-First Search (DFS) in JavaScript

---

## 🚀 What is DFS?

**Depth-First Search (DFS)** is a graph traversal algorithm that explores as far as possible along each branch before backtracking.

Think of it like navigating a maze: you go as deep as you can down a path until you hit a dead end, then backtrack and try another path.

---

## 🧩 When to Use DFS?

- To explore all nodes/paths in a graph/tree
- To detect cycles in a graph
- To solve maze/pathfinding problems
- To generate topological order (in DAGs)

---

## 🧱 Graph Representation

We use a **Map** object to represent the adjacency list.

### 🔢 Input Data

```javascript
const edges = [
  [0, 1, 5, 7],
  [1, 0, 2],
  [2, 1, 8, 3],
  [3, 2, 11, 4],
  [4, 3],
  [5, 0, 6],
  [6, 5, 7, 0],
  [7, 0],
  [8, 2, 9, 10],
  [9, 8],
  [10, 8],
  [11, 3],
];
```

This means:
- Node 0 is connected to 1, 5, 7
- Node 1 is connected to 0, 2
- ... and so on.

---

## 🔨 Convert to Adjacency List

```javascript
function inputToList(edges) {
  const edgeList = new Map();
  for (let val of edges) {
    let [mapKey, ...mapVal] = val;
    edgeList.set(mapKey, mapVal);
  }
  return edgeList;
}
```

---

## 🧠 DFS Logic (Recursive Approach)

```javascript
function dfs(source, neighbours, edgeList, visited = [], result = []) {
  if (!visited[source]) {
    result.push(source);
    visited[source] = true;
  }

  for (let i = 0; i < neighbours.length; i++) {
    let currVal = neighbours[i];
    if (!visited[currVal]) {
      dfs(currVal, edgeList.get(currVal), edgeList, visited, result);
    }
  }

  return result;
}
```

---

## 🔄 Flowchart (Text Diagram)

```
Start from 0
↓
Visit 0 → result = [0]
→ Go to 1 → Visit 1
  → Go to 2 → Visit 2
    → Go to 8 → Visit 8
      → Go to 9 → Visit 9
      ← Backtrack
      → Go to 10 → Visit 10
    ← Backtrack
    → Go to 3 → Visit 3
      → Go to 11 → Visit 11
      ← Backtrack
      → Go to 4 → Visit 4
← Backtrack
→ Go to 5 → Visit 5
  → Go to 6 → Visit 6
    → Go to 7 → Visit 7
```

---

## ✅ Final Output

```javascript
const result = dfs(0, edgeList.get(0), edgeList);
console.log("result: ", result);
```

🟢 Sample Output:
```
Result: [0, 1, 2, 8, 9, 10, 3, 11, 4, 5, 6, 7]
```

---

## 📌 Complete Code (Copy-Paste Friendly)

```javascript
console.log("Graph");

function main() {
  const edges = [
    [0, 1, 5, 7],
    [1, 0, 2],
    [2, 1, 8, 3],
    [3, 2, 11, 4],
    [4, 3],
    [5, 0, 6],
    [6, 5, 7, 0],
    [7, 0],
    [8, 2, 9, 10],
    [9, 8],
    [10, 8],
    [11, 3],
  ];

  const edgeList = inputToList(edges);
  const result = dfs(0, edgeList.get(0), edgeList);
  console.log("result: ", result);
}

function inputToList(edges) {
  const edgeList = new Map();
  for (let val of edges) {
    let [mapKey, ...mapVal] = val;
    edgeList.set(mapKey, mapVal);
  }
  return edgeList;
}

function dfs(source, neighbours, edgeList, visited = [], result = []) {
  if (!visited[source]) {
    result.push(source);
    visited[source] = true;
  }

  for (let i = 0; i < neighbours.length; i++) {
    let currVal = neighbours[i];
    if (!visited[currVal]) {
      dfs(currVal, edgeList.get(currVal), edgeList, visited, result);
    }
  }

  return result;
}

main();
```

---

## 📊 Visual Structure (Graph Sketch)

```
       0
     / | \
    1  5  7
    |   \
    2    6
   / \
  8   3
 / \   \
9  10   11
         |
         4
```

---

## 🔍 Summary

| Concept        | Description                                      |
|----------------|--------------------------------------------------|
| Data Structure | Recursion + Visited Array                        |
| Graph Type     | Undirected, unweighted                           |
| Visited Check  | Prevents re-visiting                             |
| Use Case       | Maze solving, full exploration, path finding     |

---

> Built for curious minds who love to explore paths deep into logic 🧠💡
