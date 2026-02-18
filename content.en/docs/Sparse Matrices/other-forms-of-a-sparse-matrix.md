---
title: Other Forms of a Sparse Matrix
weight: 7
---

A square sparse matrix can be of following types:

| Type | Description |
|:---|:---|
| **Diagonal** | Where the non-zero elements are stored on the leading diagonal of the matrix. |
| **Tridiagonal** | Where the non-zero elements are placed below or above the leading diagonal. |
| **Lower Triangular** | Where the non-zero elements are placed below the leading diagonal. |
| **Upper Triangular** | Where the non-zero elements are placed above the leading diagonal. |

Figure 4-3 illustrates these four matrices.

**Figure 4-3: Different forms of Sparse matrices**

```
Diagonal Matrix          Tridiagonal Matrix
┌───┬───┬───┬───┐       ┌───┬───┬───┬───┐
│ 4 │ 0 │ 0 │ 0 │       │ 0 │ 3 │ 0 │ 0 │
├───┼───┼───┼───┤       ├───┼───┼───┼───┤
│ 0 │ 1 │ 0 │ 0 │       │ 0 │ 0 │ 8 │ 0 │
├───┼───┼───┼───┤       ├───┼───┼───┼───┤
│ 0 │ 0 │ 9 │ 0 │       │ 0 │ 0 │ 0 │ 5 │
├───┼───┼───┼───┤       ├───┼───┼───┼───┤
│ 0 │ 0 │ 0 │12 │       │ 0 │ 0 │ 0 │ 0 │
└───┴───┴───┴───┘       └───┴───┴───┴───┘

Lower Triangular Matrix  Upper Triangular Matrix
┌───┬───┬───┬───┐       ┌───┬───┬───┬───┐
│ 0 │ 0 │ 0 │ 0 │       │ 0 │ 4 │ 0 │ 3 │
├───┼───┼───┼───┤       ├───┼───┼───┼───┤
│13 │ 0 │ 0 │ 0 │       │ 0 │ 0 │ 1 │ 0 │
├───┼───┼───┼───┤       ├───┼───┼───┼───┤
│ 9 │ 2 │ 0 │ 0 │       │ 0 │ 0 │ 0 │ 9 │
├───┼───┼───┼───┤       ├───┼───┼───┼───┤
│ 6 │ 0 │12 │ 0 │       │ 0 │ 0 │ 0 │ 0 │
└───┴───┴───┴───┘       └───┴───┴───┴───┘
```

---