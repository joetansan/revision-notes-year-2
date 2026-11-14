# 📚 IT2X11 Data Structures & Algorithms — Test 2 Study Guide
## Topics 5–9 | Complete Revision Notes

> **Exam Format:** 10 MCQs (1 mark each) + 1 Structured Question on Expression Conversion (5 marks) = **15 marks total**
>
> **MCQ Focus:** Definitions, characteristics, comparisons, identifying correct/incorrect statements
> **Structured Focus:** Infix → Prefix / Postfix conversion using the fully-parenthesise method

---

## Table of Contents

1. [Topic 5 — Recursion](#topic-5--recursion)
2. [Topic 6 — Advanced Sorting (Merge Sort & Quick Sort)](#topic-6--advanced-sorting)
3. [Topic 7 — Array-Based Sequences](#topic-7--array-based-sequences)
4. [Topic 8 — Stacks](#topic-8--stacks)
5. [Topic 9 — Queues](#topic-9--queues)
6. [Quick-Fire Comparison Tables](#quick-fire-comparison-tables)
7. [Structured Question Walkthrough](#structured-question-walkthrough)
8. [Professor's Favourite Traps](#professors-favourite-traps)

---

# Topic 5 — Recursion

## 5.1 What Is Recursion?

Recursion is a process where a **function calls itself** to solve a smaller version of the same problem.

> **Professor's wording (MCQ-ready):**
> Recursion = "A function calls itself to solve smaller instances of the same problem."

Every recursive function has **two essential parts:**

```
┌─────────────────────────────────────────────┐
│           RECURSIVE FUNCTION                │
│                                             │
│  ┌───────────────┐   ┌───────────────────┐  │
│  │  BASE CASE    │   │  RECURSIVE CASE   │  │
│  │               │   │                   │  │
│  │ Stopping      │   │ Function calls    │  │
│  │ condition.    │   │ itself with a     │  │
│  │ Prevents      │   │ SIMPLER argument  │  │
│  │ infinite      │   │ that moves       │  │
│  │ recursion.    │   │ TOWARD the       │  │
│  │               │   │ base case.       │  │
│  └───────────────┘   └───────────────────┘  │
└─────────────────────────────────────────────┘
```

### Key Terms to Memorise

| Term | Definition |
|------|-----------|
| **Base case** | The stopping condition. Returns a value directly without further recursion. |
| **Recursive case** | The part where the function calls itself with a *simpler* (closer to base case) argument. |
| **Stack overflow** | What happens when there's NO base case — the function keeps calling itself until the runtime stack runs out of memory. |

## 5.2 Example: Factorial

```
factorial(n)
│
├─ Base case:    n == 0  →  return 1
│
└─ Recursive case: n * factorial(n-1)
```

**Trace for factorial(4):**

```
factorial(4)
  = 4 * factorial(3)
  = 4 * (3 * factorial(2))
  = 4 * (3 * (2 * factorial(1)))
  = 4 * (3 * (2 * (1 * factorial(0))))
  = 4 * (3 * (2 * (1 * 1)))      ← base case hit
  = 4 * (3 * (2 * 1))
  = 4 * (3 * 2)
  = 4 * 6
  = 24
```

**Time complexity:** O(n) — one call per value from n down to 0.

## 5.3 Recursion Call Tree

A **call tree** is a diagram showing how recursive calls branch out.

```
              factorial(4)            ← root
               /        \
         4 * factorial(3)
                /        \
          3 * factorial(2)
                 /        \
           2 * factorial(1)
                  /        \
            1 * factorial(0)
                        |
                       [1]          ← leaf (base case)
```

**Vocabulary for the tree:**

| Term | Meaning |
|------|---------|
| **Node** | Each function call |
| **Branch** | A recursive call from parent to child |
| **Leaf** | A call that hits the base case (no further recursion) |
| **Call depth** | How many levels deep the tree goes |

## 5.4 The Runtime Stack

The computer uses a **stack** (LIFO — Last In, First Out) to manage recursive calls.

```
When factorial(4) is called:

    ┌─────────────────┐
    │ factorial(0)     │  ← pushed last, executes first (top of stack)
    ├─────────────────┤
    │ factorial(1)     │
    ├─────────────────┤
    │ factorial(2)     │
    ├─────────────────┤
    │ factorial(3)     │
    ├─────────────────┤
    │ factorial(4)     │  ← pushed first, executes last (bottom)
    └─────────────────┘
          RUNTIME STACK
```

Each **activation record** (stack frame) stores:

- **Parameters** (e.g., n = 4)
- **Local variables**
- **Return address** (where to continue after the call returns)

When a function **returns**, its activation record is **popped** off the stack.

> **MCQ trap:** "What happens without a base case?" → **Stack overflow** (infinite recursion)

## 5.5 Recursion vs Iteration

| Aspect | Recursion | Iteration |
|--------|-----------|-----------|
| **Mechanism** | Function calls itself | Loop (for/while) |
| **Best for** | Tree traversal, backtracking, hierarchical data, divide-and-conquer | Fixed repetitions, flat/linear data |
| **Memory** | Uses call stack (more memory) | Uses loop variables (less memory) |
| **Readability** | Often more elegant for naturally recursive problems | More explicit, sometimes clearer |
| **Risk** | Stack overflow if no base case | Infinite loop if no exit condition |

> **Connection to later topics:** Recursion is the *engine* behind Merge Sort and Quick Sort (Topic 6). The runtime stack managing recursive calls is the same stack data structure we study in Topic 8.

## 5.6 Practical Recursion Patterns

```
countDigits(n):        sumDigits(n):         productDigits(n):
  if n < 10:             if n < 10:            if n < 10:
    return 1               return n              return n
  return 1 +             return (n%10)         return (n%10) *
         countDigits(n//10)       +                    productDigits(n//10)
                          sumDigits(n//10)
```

**is_sorted(lst):**
```
is_sorted(lst, i=0):
  if i == len(lst) - 1:    return True       # base case
  if lst[i] > lst[i+1]:    return False      # not sorted
  return is_sorted(lst, i+1)                  # check next pair
```

---

# Topic 6 — Advanced Sorting

## 6.1 The Divide-and-Conquer Paradigm

Both Merge Sort and Quick Sort follow the same three-step pattern:

```
┌──────────────────────────────────────────────┐
│          DIVIDE AND CONQUER                  │
│                                              │
│  Step 1: DIVIDE                              │
│     Split the problem into smaller           │
│     subproblems                              │
│                                              │
│  Step 2: RECUR                               │
│     Solve each subproblem                    │
│     recursively                              │
│                                              │
│  Step 3: CONQUER                             │
│     Combine the solutions of the             │
│     subproblems to get the final answer      │
└──────────────────────────────────────────────┘
```

## 6.2 Why Not Just Use Basic Sorts?

| Algorithm | Time (Average) | Time (Worst) | Problem |
|-----------|---------------|-------------|---------|
| Bubble Sort | O(n²) | O(n²) | Too slow for large datasets |
| Selection Sort | O(n²) | O(n²) | Too slow for large datasets |
| Insertion Sort | O(n²) | O(n²) | Too slow for large datasets |

**O(n²)** means if n doubles, time quadruples. For 10,000 items that's 100,000,000 operations — unacceptable for real applications. That's why we need **O(n log n)** sorts.

## 6.3 Merge Sort

### How It Works

```
         [38, 27, 43, 3, 9, 82, 10]
                     │
           ┌─────────┴──────────┐
      [38, 27, 43, 3]     [9, 82, 10]
           │                     │
     ┌─────┴─────┐         ┌─────┴─────┐
  [38, 27]   [43, 3]    [9, 82]    [10]     ← base case (1 element)
     │          │          │         │
  ┌──┴──┐   ┌──┴──┐    ┌──┴──┐      │
 [38]  [27] [43]  [3]  [9]  [82]   [10]
  └──┬──┘   └──┬──┘    └──┬──┘      │
  [27,38]   [3,43]     [9,82]    [10]
     └─────┬─────┘     └────┬──────┘
      [3, 27, 38, 43]    [9, 10, 82]
           └──────────┬──────────┘
           [3, 9, 10, 27, 38, 43, 82]
```

### The Merge Step (this is the key operation)

```
Merging [27, 38] and [3, 43]:

  Left: [27, 38]     Right: [3, 43]
         ↑                    ↑
        i=0                  j=0

  Compare 27 vs 3 → 3 is smaller → take 3    Result: [3]
  Compare 27 vs 43 → 27 is smaller → take 27  Result: [3, 27]
  Compare 38 vs 43 → 38 is smaller → take 38  Result: [3, 27, 38]
  Right has 43 left → take 43                  Result: [3, 27, 38, 43]
```

### Merge Sort Summary

| Property | Value |
|----------|-------|
| **Strategy** | Divide into halves → Recur on each half → Merge sorted halves |
| **Base case** | List with 0 or 1 elements (already sorted) |
| **Time — Best** | O(n log n) |
| **Time — Average** | O(n log n) |
| **Time — Worst** | O(n log n) ← **consistent!** |
| **Space** | O(n) extra memory for merging |
| **Stable?** | ✅ Yes — equal elements keep original order |
| **In-place?** | ❌ No — needs extra arrays for merging |

## 6.4 Quick Sort

### How It Works

```
         [38, 27, 43, 3, 9, 82, 10]
                pivot = 38
                    │
        ┌───────────┼───────────┐
   [< 38]         [38]        [> 38]
  [27,3,9,10]     [38]      [43,82]
       │                        │
   pivot=27                  pivot=43
       │                        │
  ┌────┼────┐              ┌────┼────┐
[3,9] [27] [10]         [43] [43] [82]
  │         │
pivot=3  pivot=10
  │         │
┌─┼─┐    ┌──┼──┐
[3][3][9] [10][10][]

Final: [3, 9, 10, 27, 38, 43, 82]
```

### The Partition Step

```
Array: [38, 27, 43, 3, 9, 82, 10]    pivot = 38

Elements < 38:  [27, 3, 9, 10]
Elements = 38:  [38]
Elements > 38:  [43, 82]

Recombine: [27, 3, 9, 10, 38, 43, 82]
            └──── left ────┘   └─ right ─┘
```

### Quick Sort Summary

| Property | Value |
|----------|-------|
| **Strategy** | Pick pivot → Partition (< pivot, = pivot, > pivot) → Recur on partitions |
| **Base case** | first >= last (subarray of size 0 or 1) |
| **Time — Best** | O(n log n) |
| **Time — Average** | O(n log n) |
| **Time — Worst** | O(n²) — when pivot is always min or max (already sorted data!) |
| **Space** | O(log n) for recursion stack |
| **Stable?** | ❌ No — partitioning can reorder equal elements |
| **In-place?** | ✅ Yes — rearranges within original array |

## 6.5 Merge Sort vs Quick Sort — Side by Side

| Feature | Merge Sort | Quick Sort |
|---------|-----------|------------|
| **Divide step** | Split into halves | Partition around pivot |
| **Conquer step** | Merge sorted lists | Concatenate partitions |
| **Time (worst)** | O(n log n) ✅ | O(n²) ❌ |
| **Time (avg)** | O(n log n) | O(n log n) |
| **Extra memory** | O(n) | O(log n) |
| **In-place** | ❌ No | ✅ Yes |
| **Stable** | ✅ Yes | ❌ No |
| **Best for** | Linked lists, need stability, guaranteed performance | In-memory sorting, memory-constrained, large random data |

> **MCQ favourite:** "Which sort is guaranteed O(n log n) in ALL cases?" → **Merge Sort**
>
> "Which sort is in-place?" → **Quick Sort**
>
> "Which sort is stable?" → **Merge Sort**

### What Is Stability?

```
Original:  [A1, B1, A2, B2]   (where A1 and A2 have the same key)

Stable sort:   A1 always comes before A2  ✓ (preserves original order)
Unstable sort: A1 might come after A2     ✗ (order not guaranteed)
```

### What Is In-Place?

**In-place** = the algorithm rearranges elements within the original array using only O(1) or O(log n) extra memory (not counting the input).

---

# Topic 7 — Array-Based Sequences

## 7.1 Python Sequence Types

Python has three main **array-based** sequence types:

| Type | Mutable? | Example | Use Case |
|------|----------|---------|----------|
| `list` | ✅ Yes | `[1, 2, 3]` | General-purpose, can modify |
| `tuple` | ❌ No | `(1, 2, 3)` | Fixed data, immutable |
| `str` | ❌ No | `"hello"` | Text, immutable |

All three use **zero-based indexing** and support **contiguous memory storage**.

## 7.2 Zero-Based Indexing

```
Array:    [10, 20, 30, 40, 50]
Index:      0   1   2   3   4
Negative:  -5  -4  -3  -2  -1

First element:  index 0    (or -len)
Last element:   index -1   (or len-1)
```

## 7.3 Memory Layout & Direct Access

Arrays store elements in **contiguous memory** — this is why we get **O(1) random access**.

```
Memory Address Formula:

    Address = Base Address + (Index × Element Size)

Example:
    Base Address = 1000
    Element Size = 4 bytes (for integers)
    
    Index 0: 1000 + (0 × 4) = 1000
    Index 1: 1000 + (1 × 4) = 1004
    Index 2: 1000 + (2 × 4) = 1008
    Index 5: 1000 + (5 × 4) = 1020
```

```
Visual:

    Memory:
    ┌──────┬──────┬──────┬──────┬──────┐
    │  10  │  20  │  30  │  40  │  50  │
    └──────┴──────┴──────┴──────┴──────┘
    1000   1004   1008   1012   1016
    
    Direct access to index 3:
    1000 + (3 × 4) = 1012  →  value is 40    O(1)!
```

## 7.4 Primitive vs Referential Arrays

### Compact (Primitive) Array
Stores **actual values** directly in memory.

```
Compact array of integers:
┌────┬────┬────┬────┐
│ 10 │ 20 │ 30 │ 40 │   ← actual values stored here
└────┴────┴────┴────┘
```

### Referential Array
Stores **references (pointers)** to objects elsewhere in memory.

```
Referential array (like Python list):
┌──────────┬──────────┬──────────┬──────────┐
│ ref ──→  │ ref ──→  │ ref ──→  │ ref ──→  │
└────┬─────┴────┬─────┴────┬─────┴────┬─────┘
     │          │          │          │
   ┌─┴─┐     ┌─┴─┐     ┌─┴─┐     ┌─┴─┐
   │ 10 │     │ 20 │     │ 30 │     │ 40 │  ← objects in heap
   └────┘     └────┘     └────┘     └────┘
```

> **Key insight:** Python lists are **referential arrays**. Each slot stores a *reference* (pointer) to an object, not the object itself.

## 7.5 Python `array` Module

For compact arrays in Python, use the `array` module:

```python
from array import array

arr = array('i', [1, 2, 3, 4])   # 'i' = signed integer
arr = array('f', [1.0, 2.5])     # 'f' = float
arr = array('u', 'hello')        # 'u' = unicode character
```

| Type Code | Meaning |
|-----------|---------|
| `'i'` | Signed integer |
| `'f'` | Float |
| `'u'` | Unicode character |

**Restriction:** All elements must be the **same type** (unlike Python lists).

## 7.6 Insertion and Removal

### Insert at Index i

```
Insert 99 at index 2 in [10, 20, 30, 40, 50]:

Before: [10, 20, 30, 40, 50]
                  ↓ shift right →→→→
After:  [10, 20, 99, 30, 40, 50, __]

Time: O(n) worst case (shifting all elements)
```

### Append at End

```
Append 99 to [10, 20, 30, 40, 50]:

Before: [10, 20, 30, 40, 50]
After:  [10, 20, 30, 40, 50, 99]

Time: O(1)  ← no shifting needed!
```

### Remove at Index i

```
Remove element at index 2 from [10, 20, 30, 40, 50]:

Before: [10, 20, 30, 40, 50]
                  ←←← shift left
After:  [10, 20, 40, 50]

Time: O(n) worst case
```

### Remove Last

```
Remove last from [10, 20, 30, 40, 50]:

After:  [10, 20, 30, 40]

Time: O(1)
```

| Operation | Best Case | Worst Case |
|-----------|-----------|------------|
| Access by index | O(1) | O(1) |
| Insert at index i | O(1) end | O(n) |
| Append at end | O(1) | O(1)* |
| Remove at index i | O(1) end | O(n) |
| Remove last | O(1) | O(1) |

*Amortised O(1) when using doubling strategy

## 7.7 Dynamic Arrays

A dynamic array has two measurements:

- **Size** = number of items currently stored
- **Capacity** = total storage available

```
Example: Size=5, Capacity=8

    ┌────┬────┬────┬────┬────┬────┬────┬────┐
    │ 10 │ 20 │ 30 │ 40 │ 50 │    │    │    │
    └────┴────┴────┴────┴────┴────┴────┴────┘
    ├── used (size=5) ──┤├── spare (capacity=8) ─┤
```

### When Array Is Full — Resize!

```
What happens when we add to a full array:

1. Allocate a NEW, LARGER array
2. COPY all elements from old array to new array
3. Add the new element
4. Old array is garbage collected

    Old (full):     [10, 20, 30, 40]     capacity=4
                         ↓
    New (larger):   [10, 20, 30, 40, 50, __, __, __]    capacity=8
```

**Why allocate MORE than we need?** → To support future appends efficiently without resizing every single time.

### Two Resizing Strategies

#### Incremental Resizing (add fixed amount)

```
Add 4 extra slots each time:
Capacity: 4 → 8 → 12 → 16 → 20 → ...

Copying cost each time: 4, 8, 12, 16, ...
After n appends: 4 + 8 + 12 + ... ≈ O(n²)  TOTAL cost
```

❌ Bad — resizes too often, O(n²) total cost.

#### Doubling Strategy (industry standard)

```
Double the capacity each time:
Capacity: 1 → 2 → 4 → 8 → 16 → 32 → ...

Copying cost each time: 1, 2, 4, 8, 16, ...
After n appends: 1 + 2 + 4 + 8 + ... ≈ 2n ≈ O(n)  TOTAL cost
```

✅ Good — O(n) total cost → **O(1) amortised per append**.

> **MCQ favourite:** "What is the amortised cost per append using the doubling strategy?" → **O(1)**
>
> "What's the total cost of n appends with incremental resizing?" → **O(n²)**

## 7.8 Shallow Copy

```
Original list:  A = [1, 2, 3]
Shallow copy:   B = A.copy()   or   B = list(A)

    A ──→ [ ● | ● | ● ]     ← A's internal array
              │   │   │
              ▼   ▼   ▼
            [1] [2] [3]       ← shared objects (integers are immutable, so OK)

    B ──→ [ ● | ● | ● ]     ← B's NEW internal array
              │   │   │
              └─┬─┘─┬─┘
                ▼   ▼
              [1] [2] [3]    ← SAME objects as A!
```

**Shallow copy:** Creates a new array object, but elements inside point to the **same objects** as the original.

**For immutable objects** (like integers), this is fine — you can't change them anyway.

## 7.9 The `[0] * 8` Trick

```python
row = [0] * 8
# Result: [0, 0, 0, 0, 0, 0, 0, 0]
```

This creates a **referential array** where all 8 slots point to the **same** integer object `0`. This is safe because integers are **immutable**.

⚠️ **Dangerous with mutable objects:**
```python
grid = [[0] * 3] * 3   # DON'T DO THIS for 2D arrays!
# All 3 rows point to the SAME list object!
grid[0][0] = 99
# ALL rows are now [99, 0, 0] — modifying one modifies all!
```

---

# Topic 8 — Stacks

## 8.1 What Is a Stack?

A stack is a **linear data structure** where items are added and removed from **one end only** (called the **top**).

> **MCQ definition:** Stack = "A linear data structure that follows the Last-In, First-Out (LIFO) principle."

```
        ┌─────────┐
        │   TOP   │  ← push/pop here
        ├─────────┤
        │  item C │  ← last in, first out
        ├─────────┤
        │  item B │
        ├─────────┤
        │  item A │  ← first in, last out
        └─────────┘

    Push D:         Pop:
    ┌─────────┐     ┌─────────┐
    │  item D │     │   TOP   │
    ├─────────┤     ├─────────┤
    │  item C │     │  item C │  ← new top
    ├─────────┤     ├─────────┤
    │  item B │     │  item B │
    ├─────────┤     ├─────────┤
    │  item A │     │  item A │
    └─────────┘     └─────────┘
```

## 8.2 Stack Operations

| Operation | Description | Time |
|-----------|-------------|------|
| `push(item)` | Add item to the **top** | O(1) |
| `pop()` | Remove and return item from the **top** | O(1) |
| `peek()` | View the top item **without removing** it | O(1) |
| `isEmpty()` | Check if the stack is empty | O(1) |
| `__len__()` | Return number of items | O(1) |

> **Error handling:** Always check `isEmpty()` before `pop()` or `peek()` — otherwise assertion error!

## 8.3 Real-World Stack Examples

| Scenario | Why Stack? |
|----------|-----------|
| **Undo feature** (Ctrl+Z) | Last action undone first |
| **Browser back button** | Most recent page visited is the first to go back to |
| **Function call stack** | Most recently called function returns first |
| **Balanced brackets** | Push opening, pop on closing |

> **NOT a stack:** Queue at a ticket counter (FIFO), playlist shuffle (random)

## 8.4 Stack ADT vs Implementation

- **ADT (Abstract Data Type):** Defines *what* operations exist (push, pop, peek) without saying *how*
- **Implementation:** Defines *how* those operations work (using a list, linked list, etc.)

## 8.5 Python Stack Implementation

```python
class Stack:
    def __init__(self):
        self._theItems = list()    # internal list

    def isEmpty(self):
        return len(self._theItems) == 0

    def __len__(self):
        return len(self._theItems)

    def peek(self):
        assert not self.isEmpty(), "Stack is empty"
        return self._theItems[-1]

    def push(self, item):
        self._theItems.append(item)     # append = O(1)

    def pop(self):
        assert not self.isEmpty(), "Stack is empty"
        return self._theItems.pop()     # pop from end = O(1)
```

**Key insight:** Using Python's `list.append()` and `list.pop()` (from the END) gives us O(1) for both push and pop. Don't use `pop(0)` — that's O(n)!

## 8.6 Expression Notations

This is the **most testable topic** for the structured question (5 marks)!

### Three Ways to Write Expressions

| Notation | Format | Example | Needs Parentheses? |
|----------|--------|---------|-------------------|
| **Infix** | operator BETWEEN operands | `A + B` | ✅ Yes (ambiguous otherwise) |
| **Prefix** | operator BEFORE operands | `+ A B` | ❌ No |
| **Postfix** | operator AFTER operands | `A B +` | ❌ No |

```
Infix:      A + B
            ═══════
Prefix:   + A B          (operator at FRONT)
          ═

Postfix:  A B +          (operator at BACK)
                ═
```

### More Examples

| Infix | Prefix | Postfix |
|-------|--------|---------|
| `A + B` | `+ A B` | `A B +` |
| `A + B * C` | `+ A * B C` | `A B C * +` |
| `(A + B) * C` | `* + A B C` | `A B + C *` |

## 8.7 Infix → Postfix / Prefix Conversion

### Step-by-Step Method

**Step 1:** Fully parenthesise the expression (add parentheses for every operation, respecting precedence)

**Step 2:** Move each operator:
- **Prefix:** Move operator to **just before** its opening parenthesis
- **Postfix:** Move operator to **just after** its closing parenthesis

**Step 3:** Remove all parentheses

### Operator Precedence (remember this!)

```
Highest:  ^ (exponentiation)
Middle:   * / (multiplication, division)
Lowest:   + - (addition, subtraction)

Associativity:
  +, -, *, /  →  Left to Right
  ^            →  Right to Left
```

### Example 1: `A * B + C / D`

**Step 1 — Fully parenthesise:**

```
Original:    A * B + C / D

Precedence:  * and / are higher than +

             ((A * B) + (C / D))
```

**Step 2a — To Postfix** (move operator to AFTER closing paren):

```
((A * B) + (C / D))
         ↓
(A B *) + (C D /)
             ↓
(A B *)(C D /) +
         ↓
A B * C D / +
```

**Postfix: `A B * C D / +`**

**Step 2b — To Prefix** (move operator to BEFORE opening paren):

```
((A * B) + (C / D))
 ↓
(+ (A B *) (C D /))
 ↓
+ * A B / C D
```

**Prefix: `+ * A B / C D`**

### Example 2: `A * (B + C) / D`

**Step 1 — Fully parenthesise:**

```
Original:    A * (B + C) / D

Precedence:  * and / are same level, left to right
             (B + C) already has parentheses

             ((A * (B + C)) / D)
```

**Step 2a — To Postfix:**

```
((A * (B + C)) / D)
          ↓
(A (B C +) *) D /
          ↓
A B C + * D /
```

**Postfix: `A B C + * D /`**

**Step 2b — To Prefix:**

```
((A * (B + C)) / D)
   ↓
(/ (A * (B C +)) D)
   ↓
/ * A + B C D
```

**Prefix: `/ * A + B C D`**

## 8.8 Postfix Evaluation Using a Stack

### Algorithm

```
Scan the postfix expression left to right:
  1. If operand → PUSH onto stack
  2. If operator → POP two operands, apply operator, PUSH result
     (First popped = RIGHT operand, Second popped = LEFT operand)
```

### Example 1: Evaluate `A B C + * D /` where A=8, B=2, C=3, D=4

```
Expression: 8 2 3 + * 4 /

Step   Token   Action              Stack
────   ─────   ──────              ─────────────
 1       8     Push 8              [8]
 2       2     Push 2              [8, 2]
 3       3     Push 3              [8, 2, 3]
 4       +     Pop 3, 2            [8]
              2 + 3 = 5
              Push 5              [8, 5]
 5       *     Pop 5, 8            []
              8 * 5 = 40
              Push 40             [40]
 6       4     Push 4              [40, 4]
 7       /     Pop 4, 40           []
              40 / 4 = 10
              Push 10             [10]

Result: 10 ✓
```

### Example 2: Evaluate `5 2 3 * + 4 -`

```
Step   Token   Action              Stack
────   ─────   ──────              ─────────────
 1       5     Push 5              [5]
 2       2     Push 2              [5, 2]
 3       3     Push 3              [5, 2, 3]
 4       *     Pop 3, 2            [5]
              2 * 3 = 6
              Push 6              [5, 6]
 5       +     Pop 6, 5            []
              5 + 6 = 11
              Push 11             [11]
 6       4     Push 4              [11, 4]
 7       -     Pop 4, 11           []
              11 - 4 = 7
              Push 7              [7]

Result: 7 ✓
```

> **⚠️ CRITICAL:** "First popped = RIGHT operand" matters for subtraction and division!
>
> Stack top is 4, next is 11. We compute `11 - 4`, NOT `4 - 11`.

## 8.9 Balancing Brackets (Common Practical)

```python
def is_balanced(expr):
    stack = Stack()
    matching = {')': '(', ']': '[', '}': '{'}
    
    for char in expr:
        if char in '([{':
            stack.push(char)
        elif char in ')]}':
            if stack.isEmpty():
                return False
            if stack.pop() != matching[char]:
                return False
    
    return stack.isEmpty()
```

---

# Topic 9 — Queues

## 9.1 What Is a Queue?

A queue is a **linear data structure** where items are added at one end (**back/rear**) and removed from the other end (**front**).

> **MCQ definition:** Queue = "A linear data structure that follows the First-In, First-Out (FIFO) principle."

```
    ENQUEUE here                    DEQUEUE here
         │                               │
         ▼                               ▼
    ┌────┬────┬────┬────┬────┬────┐
    │    │    │  C │  B │  A │    │
    └────┴────┴────┴────┴────┴────┘
                      back   front
    
    Back →  where new items join
    Front → where items leave
    
    ENQUEUE D:
    ┌────┬────┬────┬────┬────┬────┐
    │    │    │    │  D │  C │  B │  A was dequeued
    └────┴────┴────┴────┴────┴────┘
```

## 9.2 Queue Operations

| Operation | Description | Time |
|-----------|-------------|------|
| `enqueue(item)` | Add item to the **back** | O(1)* |
| `dequeue()` | Remove and return item from the **front** | O(n)† |
| `isEmpty()` | Check if queue is empty | O(1) |
| `__len__()` | Return number of items | O(1) |

*O(1) with list append
†O(n) with `pop(0)` due to shifting; O(1) with circular array

## 9.3 Real-World Queue Examples

| Scenario | Why Queue? |
|----------|-----------|
| **Print spooling** | First document sent prints first |
| **Task scheduling** | First task queued runs first |
| **Web server requests** | First request served first |
| **BFS (Breadth-First Search)** | Explores nodes level by level |

> **NOT a queue:** Undo feature (that's a stack — LIFO)

## 9.4 Stack vs Queue — The Key Comparison

```
STACK (LIFO):                    QUEUE (FIFO):
                                    
    ┌─────────┐                   Back ──→  ┌────┬────┬────┬────┐  ←── Front
    │   TOP   │                             │  D │  C │  B │  A │
    ├─────────┤                             └────┴────┴────┴────┘
    │  push → │                                  enqueue →    → dequeue
    │  pop  → │
    ├─────────┤
    │  item B │
    ├─────────┤
    │  item A │
    └─────────┘
  One end (top)                   Two ends (front + back)
  Last in, First out              First in, First out
```

| Feature | Stack | Queue |
|---------|-------|-------|
| **Principle** | LIFO | FIFO |
| **Ends** | One (top) | Two (front + back) |
| **Add** | push (to top) | enqueue (to back) |
| **Remove** | pop (from top) | dequeue (from front) |

## 9.5 Simple Python List Queue Implementation

```python
class Queue:
    def __init__(self):
        self._theItems = list()

    def isEmpty(self):
        return len(self._theItems) == 0

    def __len__(self):
        return len(self._theItems)

    def enqueue(self, item):
        self._theItems.append(item)       # O(1)

    def dequeue(self):
        assert not self.isEmpty(), "Queue is empty"
        return self._theItems.pop(0)      # O(n) — shifting!
```

**Problem:** `pop(0)` is O(n) because every remaining element must shift left.

## 9.6 Circular Array Queue

A **circular array** wraps around so that the front and back can be anywhere in the array.

```
Circular array of size 6:

After enqueue A, B, C, D:
    Index:  0    1    2    3    4    5
         [  A ][  B ][  C ][  D ][    ][    ]
           ↑                        ↑
         front=0                  back=3

After dequeue A, dequeue B, enqueue E, enqueue F:
    Index:  0    1    2    3    4    5
         [    ][    ][  C ][  D ][  E ][  F ]
                            ↑         ↑
                          front=2   back=5

After enqueue G (wraps around!):
    Index:  0    1    2    3    4    5
         [  G ][    ][  C ][  D ][  E ][  F ]
           ↑
         back=0  ← wrapped around!
                       front=2
```

### Wrap-Around Arithmetic

```python
# After enqueue, advance back pointer:
back = (back + 1) % array_size

# After dequeue, advance front pointer:
front = (front + 1) % array_size
```

```
Example: array_size = 6

If back = 5, next position = (5 + 1) % 6 = 0  ← wraps to start!
If front = 5, next position = (5 + 1) % 6 = 0
```

### Full and Empty Conditions

```
Empty:  count == 0      (front and back positions don't matter)
Full:   count == array_size   (all slots occupied)
```

### Circular Queue Implementation

```python
class CircularQueue:
    def __init__(self, size):
        self._array = [None] * size
        self._size = size
        self._front = 0
        self._back = -1       # or size - 1
        self._count = 0

    def isEmpty(self):
        return self._count == 0

    def isFull(self):
        return self._count == self._size

    def __len__(self):
        return self._count

    def enqueue(self, item):
        assert not self.isFull(), "Queue is full"
        self._back = (self._back + 1) % self._size
        self._array[self._back] = item
        self._count += 1

    def dequeue(self):
        assert not self.isEmpty(), "Queue is empty"
        item = self._array[self._front]
        self._front = (self._front + 1) % self._size
        self._count -= 1
        return item
```

### Circular Queue Advantages & Disadvantages

| Advantages | Disadvantages |
|-----------|--------------|
| O(1) for both enqueue and dequeue | Fixed capacity (must know max size) |
| No shifting needed | More complex pointer management |
| Memory efficient (reuses empty slots) | Wrap-around logic can be error-prone |

> **MCQ favourite:** "What is the main advantage of a circular array queue over a simple list queue?" → **O(1) for both enqueue and dequeue (no shifting)**

---

# Quick-Fire Comparison Tables

## All Data Structures Compared

| Feature | Stack | Queue | Array |
|---------|-------|-------|-------|
| **Principle** | LIFO | FIFO | Random access |
| **Add** | O(1) push | O(1) enqueue | O(1) append, O(n) insert at i |
| **Remove** | O(1) pop | O(1) dequeue* | O(1) remove last, O(n) remove at i |
| **Access** | O(1) peek (top only) | O(1) front only | O(1) any index |
| **Use cases** | Undo, call stack, brackets | Scheduling, BFS, print queue | General storage, indexing |

*Circular array implementation

## All Sorting Algorithms Compared

| Algorithm | Best | Average | Worst | Stable | In-Place | Extra Space |
|-----------|------|---------|-------|--------|----------|-------------|
| Bubble | O(n) | O(n²) | O(n²) | ✅ | ✅ | O(1) |
| Selection | O(n²) | O(n²) | O(n²) | ❌ | ✅ | O(1) |
| Insertion | O(n) | O(n²) | O(n²) | ✅ | ✅ | O(1) |
| **Merge** | O(n log n) | O(n log n) | O(n log n) | ✅ | ❌ | O(n) |
| **Quick** | O(n log n) | O(n log n) | O(n²) | ❌ | ✅ | O(log n) |

## Array Resizing Strategies

| Strategy | Resize Trigger | Total Cost (n adds) | Amortised per Add |
|----------|---------------|--------------------|--------------------|
| Incremental (+fixed) | Add k extra slots | O(n²) | O(n) |
| Doubling (×2) | Double capacity | O(n) | O(1) |

---

# Structured Question Walkthrough

## Full Worked Example: Convert `A + B * C - D / E` to Postfix and Prefix

### Step 1: Fully Parenthesise

```
Original: A + B * C - D / E

Operator precedence:
  * and /  →  higher
  + and -  →  lower (same level, left-to-right)

Step by step:
  1. B * C       →  (B * C)         highest precedence first
  2. D / E       →  (D / E)         same precedence
  3. A + (B*C)   →  (A + (B*C))     next level
  4. (A+(B*C)) - (D/E)  →  ((A + (B * C)) - (D / E))   final

Fully parenthesised: ((A + (B * C)) - (D / E))
```

### Step 2a: Convert to POSTFIX (move operator to AFTER closing paren)

```
((A + (B * C)) - (D / E))

Start from innermost parentheses:

1. (B * C) → B C *
   Result so far: ((A + B C *) - (D / E))

2. (D / E) → D E /
   Result so far: ((A + B C *) - D E /)

3. (A + B C *) → A B C * +
   Result so far: (A B C * + - D E /)

4. (A B C * + - D E /) → A B C * + D E / -
   Result: A B C * + D E / -
```

**Postfix: `A B C * + D E / -`**

### Step 2b: Convert to PREFIX (move operator to BEFORE opening paren)

```
((A + (B * C)) - (D / E))

Start from innermost parentheses:

1. (B * C) → * B C
   Result so far: ((A + * B C) - (D / E))

2. (D / E) → / D E
   Result so far: ((A + * B C) - / D E)

3. (A + * B C) → + A * B C
   Result so far: (+ A * B C - / D E)

4. (+ A * B C - / D E) → - + A * B C / D E
   Result: - + A * B C / D E
```

**Prefix: `- + A * B C / D E`**

### Step 3: Verify by Evaluation

Let A=6, B=2, C=3, D=10, E=5

```
Infix:   6 + 2 * 3 - 10 / 5
       = 6 + 6 - 2
       = 10

Postfix: 6 2 3 * + 10 5 / -
Step: push 6, push 2, push 3
      *: pop 3,2 → 6, push 6     stack: [6, 6]
      +: pop 6,6 → 12, push 12   stack: [12]
      push 10, push 5
      /: pop 5,10 → 2, push 2    stack: [12, 2]
      -: pop 2,12 → 10, push 10  stack: [10]
Result: 10 ✓
```

---

# Professor's Favourite Traps

## Common MCQ Tricks

### 1. Confusing Stack and Queue

```
❌ "A queue follows LIFO"           → That's a STACK
❌ "A stack has enqueue and dequeue" → Stack has PUSH and POP
✅ "A queue follows FIFO"           → Correct
✅ "A stack has push and pop"       → Correct
```

### 2. Base Case Confusion

```
❌ "Without a base case, recursion works fine"
   → WRONG: causes STACK OVERFLOW

✅ "Without a base case, infinite recursion occurs"
   → CORRECT
```

### 3. Merge Sort vs Quick Sort Stability

```
❌ "Quick Sort is stable"
   → WRONG: partitioning can reorder equal elements

✅ "Merge Sort is stable"
   → CORRECT: merging preserves relative order
```

### 4. Time Complexity Traps

```
❌ "Merge Sort is O(n²) in worst case"
   → WRONG: it's ALWAYS O(n log n)

✅ "Quick Sort is O(n²) in worst case"
   → CORRECT: when pivot is always min or max
```

### 5. In-Place Confusion

```
❌ "Merge Sort is in-place"
   → WRONG: needs O(n) extra memory

✅ "Quick Sort is in-place"
   → CORRECT: sorts within original array
```

### 6. Dynamic Array Costs

```
❌ "Appending to a dynamic array is always O(1)"
   → WRONG: when resize needed, it's O(n) for that single operation

✅ "Appending to a dynamic array is O(1) AMORTISED"
   → CORRECT: most appends are O(1), occasional resize is O(n)
```

### 7. Expression Conversion Order of Operations

```
❌ Moving operator before fully parenthesising
   → WRONG: will get wrong result

✅ Always fully parenthesise FIRST, then move operators
   → CORRECT: guarantees proper order
```

### 8. Postfix Evaluation Operand Order

```
❌ First popped = LEFT operand
   → WRONG for - and / (gives wrong result)

✅ First popped = RIGHT operand, Second popped = LEFT operand
   → CORRECT

Example: Stack has [11, 4] (4 on top)
  Pop 4 (right), Pop 11 (left)
  Compute: 11 - 4 = 7  ✓
  NOT: 4 - 11 = -7     ✗
```

### 9. What Is / Isn't a Stack or Queue

```
Stack examples:     undo, browser back, function call stack, balanced brackets
NOT stack:          queue at counter, playlist shuffle, BFS traversal

Queue examples:     print spooling, task scheduling, web server requests, BFS
NOT queue:          undo feature (that's stack), call stack (that's stack)
```

### 10. Python List as Stack/Queue

```
Stack with list:   push = append(), pop = pop()          → Both O(1) ✓
Queue with list:   enqueue = append(), dequeue = pop(0)  → dequeue is O(n) ✗
Circular array:    Both enqueue and dequeue are O(1)      → ✓
```

---

## Final Checklist Before the Exam

- [ ] Can I explain recursion in my own words?
- [ ] Do I know what happens without a base case?
- [ ] Can I draw a recursion call tree?
- [ ] Can I trace through Merge Sort step by step?
- [ ] Can I trace through Quick Sort step by step?
- [ ] Do I know which sort is stable? In-place?
- [ ] Can I calculate memory addresses in an array?
- [ ] Do I understand referential vs compact arrays?
- [ ] Can I explain the doubling strategy and its amortised cost?
- [ ] Can I convert infix to postfix by fully parenthesising?
- [ ] Can I convert infix to prefix by fully parenthesising?
- [ ] Can I evaluate a postfix expression using a stack?
- [ ] Do I know the difference between stack and queue?
- [ ] Can I implement a circular array queue with wrap-around?
- [ ] Do I know the time complexity of all operations?

---

*Good luck on Test 2! 🎯*
