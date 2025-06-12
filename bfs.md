
# 🧠 Understanding Breadth-First Search (BFS) in JavaScript

---

## 🚀 What is BFS?

**Breadth-First Search (BFS)** is a graph traversal algorithm that explores all the neighbors of a node before moving on to their neighbors.

Imagine you're exploring a city map — you first explore all directly connected cities from your current location before going further.

---

## 🧩 When to Use BFS?

- To find the shortest path (in unweighted graphs)
- To explore connected components
- To check if a graph is bipartite
- In puzzle solving (like word ladders, mazes)

---

## 🧱 Graph Representation

We use an **Adjacency List** with a `Map` object to store graph connections.

### 🔢 Input Data

```javascript
const edges = [
  [0, 1, 4, 5],
  [1, 0, 2],
  [2, 1, 9, 3],
  [3, 2],
  [4, 0, 6, 8, 7],
  [5, 0],
  [6, 4],
  [7, 4],
  [8, 4],
  [9, 2],
];
```

This means:
- Node 0 is connected to 1, 4, 5
- Node 1 is connected to 0, 2
- ... and so on.

---

## 🧮 Adjacency List Creation

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

## 🔄 BFS Logic (Step-by-step)

```javascript
function bfs(source, edgelist) {
  const visited = [];
  const que = [];
  const result = [];

  que.push(source); // Step 1: Add source

  while (que.length > 0) {
    let front = que.shift(); // Step 2: Remove front

    if (!visited[front]) {
      visited[front] = true; // Step 3: Mark as visited
      result.push(front);    // Step 4: Add to result

      let neighbours = edgelist.get(front);
      for (let val of neighbours) {
        if (!visited[val]) {
          que.push(val); // Step 5: Enqueue unvisited neighbors
        }
      }

      console.log("Queue Status: ", que.toString());
    }
  }

  return result;
}
```

---

## 🔁 Flowchart (Text Diagram)

```
Start from source
     ↓
[0] → visit → queue = [1, 4, 5]
     ↓
[1] → visit → queue = [4, 5, 2]
     ↓
[4] → visit → queue = [5, 2, 6, 8, 7]
     ↓
[5] → visit → queue = [2, 6, 8, 7]
     ↓
[2] → visit → queue = [6, 8, 7, 9, 3]
     ↓
[6] → visit → ...
```

---

## 🎯 Final Output

```javascript
const result = bfs(0, edgeList);
console.log("Result: ", result);
```

✅ Output:
```
Result: [0, 1, 4, 5, 2, 6, 8, 7, 9, 3]
```

---

## 📌 Complete Code (Copy-Paste Friendly)

```javascript
console.log("Graph");

function main() {
  const edges = [
    [0, 1, 4, 5],
    [1, 0, 2],
    [2, 1, 9, 3],
    [3, 2],
    [4, 0, 6, 8, 7],
    [5, 0],
    [6, 4],
    [7, 4],
    [8, 4],
    [9, 2],
  ];

  const edgeList = inputToList(edges);
  console.log("edgeList: ", edgeList);

  const result = bfs(0, edgeList);
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

function bfs(source, edgelist) {
  const visited = [];
  const que = [];
  const result = [];
  que.push(source);

  while (que.length > 0) {
    let front = que.shift();
    if (!visited[front]) {
      visited[front] = true;
      result.push(front);
      let neighbours = edgelist.get(front);
      for (let val of neighbours) {
        if (!visited[val]) que.push(val);
      }
      console.log("que: ", que.toString());
    }
  }

  return result;
}

main();
```

---

## 🔍 Summary

| Concept        | Description                                      |
|----------------|--------------------------------------------------|
| Data Structure | Queue (FIFO using array)                         |
| Graph Type     | Unweighted, undirected                           |
| Visited Check  | Ensures no duplicate visits                      |
| Use Case       | Shortest path, level-wise traversal              |

---

## 💡 Visual Tip


```
     0
   / | \
  1  4  5
     | \
   6  7  8
         |
         2
        / \
       3   9
```

---

## 🧠 Pro Tip

- Use `Set` instead of array for visited if graph has non-numeric nodes.
- Add `parent[]` or `distance[]` if you want path tracing or shortest path.

---

> Made for learners who think logically, visualize clearly, and code smartly 🚀
