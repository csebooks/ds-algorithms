---
title: Summary of Corrections Made
weight: 9
---

1. **Program 6-1**: Fixed incomplete sentence in introductory text ("to be able to implement" → "to be able to implement queue data structures")

2. **Program 6-2**: 
   - Added missing `#include <stdlib.h>` for `malloc()` and `free()`
   - Fixed `addq()` function: added missing `return` statement after "Queue is full" printf
   - Fixed `addq()` function: changed `q->rear = q->rear->link` to `q->rear = temp` (correct logic)
   - Fixed `delq()` function: added check to set `q->rear = NULL` when queue becomes empty
   - Fixed `delqueue()` function: added `q->rear = NULL` at the end

3. **Program 6-3**: 
   - Fixed typo in `main()`: `addq (8\ q,9)` → `addq(&q, 9)`
   - Fixed `display()` function: `printf ((n^{n}))` → `printf("\n")`

4. **Figure 6-6 description**: Changed "The value of front in our case is 7" to "The value of front in our case is 0" (to match the actual code execution where front starts at 0)

5. **Text corrections**: Fixed various incomplete sentences and formatting issues throughout the document