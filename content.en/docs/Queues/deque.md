---
title: Deque
weight: 5
---

The word **deque** is a short form of **double-ended queue** and defines a data structure in which items can be added or deleted at either the front or rear end, but no changes can be made elsewhere in the list. Thus, a deque is a generalization of both a stack and a queue. Figure 6-7 shows the representation of a deque.

**Figure 6-7: Representation of a deque**

```
Insertion →  ┌─────┬─────┬─────┬─────┬─────┐  ← Insertion
Deletion  ←  │ 34  │ 12  │ 53  │ 61  │  9  │  → Deletion
             └─────┴─────┴─────┴─────┴─────┘
               ↑                       ↑
             front                   rear
```

There are two variations of a deque:
- **Input-restricted deque**: restricts the insertion of elements at one end only, but the deletion of elements can be done at both the ends of a queue.
- **Output-restricted deque**: restricts the deletion of elements at one end only, and allows insertion to be done at both the ends of a deque.

---