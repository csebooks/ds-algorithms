---
title: Topological Sorting
weight: 8
---

Topological sorting is a special sorting technique relevant only for a **Directed Acyclic Graph (DAG)**. If a DAG is represented using an array, then after sorting for every directed edge uv, u comes before v in the array.

**Note:** For the same DAG, multiple solutions may exist. Topological sorting is **not the same as DFS**.

**Procedure:**
1. Maintain a boolean array `visited[]` initialized to false
2. Start at a vertex with in-degree 0 (no incoming edges)
3. Perform DFS-like traversal, pushing vertices onto a stack when all their adjacent vertices have been visited
4. Unwind the stack to get the topological order

**Example:**
- **DFS:** 0, 1, 4, 2, 5, 3
- **Topological sort:** 0, 3, 2, 5, 1, 4

---