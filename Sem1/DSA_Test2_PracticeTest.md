# IT2X11 — Data Structures & Algorithms: Test 2 Practice Test

**Total Marks:** 15 | **Sections:** MCQ (10 marks) + Structured (5 marks)
**Time Allowed:** 45 minutes

---

## Section A: Multiple Choice Questions (10 marks — 1 mark each)

---

**Q1.** Which of the following best describes recursion?

A. A function that calls itself to solve smaller instances of the same problem.  
B. A loop that repeats until a condition is met.  
C. A function that calls another function with the same parameters.  
D. A process that divides a problem into unrelated sub-problems.

---

**Q2.** The stack data structure operates on which principle?

A. First-In, First-Out (FIFO)  
B. Random Access  
C. Last-In, First-Out (LIFO)  
D. Priority-based ordering

---

**Q3.** What is the time complexity of Merge Sort in **all** cases (best, average, and worst)?

A. O(n)  
B. O(n log n)  
C. O(n²)  
D. O(log n)

---

**Q4.** Under what condition does Quick Sort exhibit its worst-case time complexity?

A. When the array is already sorted in ascending order  
B. When the array contains duplicate elements  
C. When the array has an even number of elements  
D. When the pivot selection consistently produces highly unbalanced partitions

---

**Q5.** What is the time complexity of accessing an element by its index in a standard array?

A. O(1) — constant time  
B. O(n) — linear time  
C. O(log n) — logarithmic time  
D. O(n²) — quadratic time

---

**Q6.** What does the `peek` operation do on a stack?

A. Removes and returns the top element  
B. Adds a new element to the top of the stack  
C. Returns the top element without removing it  
D. Returns the bottom element of the stack

---

**Q7.** How does a circular array-based queue implement wrap-around (from the last position back to the first)?

A. Using an if-statement to reset the index to zero  
B. Using modulo arithmetic (index % capacity)  
C. By physically moving all elements  
D. By creating a new array when the end is reached

---

**Q8.** Which statement about sorting stability is correct?

A. Quick Sort is a stable sorting algorithm  
B. An unstable sort preserves the relative order of equal elements  
C. Stability is irrelevant when sorting objects with multiple keys  
D. Merge Sort is a stable sorting algorithm

---

**Q9.** When a dynamic array runs out of capacity, which resizing strategy is more efficient for a sequence of repeated append operations?

A. Doubling the capacity each time  
B. Incrementing the capacity by one each time  
C. Incrementing the capacity by a fixed amount (e.g., +10) each time  
D. Tripling the capacity each time

---

**Q10.** The queue data structure operates on which principle?

A. Last-In, First-Out (LIFO)  
B. Random Access  
C. First-In, First-Out (FIFO)  
D. Priority-based ordering

---

## Section B: Structured Question (5 marks)

---

**Q11.** Consider the following infix expression:

```
A + B * C - D / E
```

**(a)** Fully parenthesize the expression according to standard operator precedence (* and / before + and −, left-to-right for equal precedence). **(1 mark)**

**(b)** Convert the fully parenthesised expression to **prefix** notation (Polish notation). Show your working steps. **(2 marks)**

**(c)** Convert the fully parenthesised expression to **postfix** notation (Reverse Polish notation). Show your working steps. **(2 marks)**

---

## Answer Key

### Section A: MCQ Answers

| Question | Correct Answer | Topic |
|----------|---------------|-------|
| Q1 | **A** | Recursion |
| Q2 | **C** | Stacks — LIFO |
| Q3 | **B** | Merge Sort complexity |
| Q4 | **D** | Quick Sort worst case |
| Q5 | **A** | Array access time |
| Q6 | **C** | Stack — peek operation |
| Q7 | **B** | Circular queue — modulo |
| Q8 | **D** | Sorting stability |
| Q9 | **A** | Dynamic array resizing |
| Q10 | **C** | Queues — FIFO |

**Answer distribution:** A × 3 | B × 2 | C × 3 | D × 2

---

### Section B: Structured Answer

#### (a) Full Parenthesization (1 mark)

Operator precedence: `*` and `/` bind tighter than `+` and `-`. Operators of equal precedence associate left-to-right.

**Step-by-step:**

1. Identify highest precedence operators: `*` (B * C) and `/` (D / E)
2. Parenthesize those first: `(B * C)` and `(D / E)`
3. Next, leftmost `+`: `A + (B * C)` → `(A + (B * C))`
4. Next, leftmost `-`: `(A + (B * C)) - (D / E)` → `((A + (B * C)) - (D / E))`

```
((A + (B * C)) - (D / E))
```

---

#### (b) Conversion to Prefix (2 marks)

**Method:** Work from the innermost parentheses outward, replacing each sub-expression with its prefix equivalent.

1. Innermost: `(B * C)` → `* B C`
2. Innermost: `(D / E)` → `/ D E`
3. Replace back: `(A + (* B C))` → `+ A * B C`
4. Replace back: `((+ A * B C) - (/ D E))` → `- + A * B C / D E`

```
Prefix: - + A * B C / D E
```

**Verification (reading right-to-left, applying operators to next two operands):**

| Read | Stack |
|------|-------|
| E | E |
| D | D, E |
| / | D/E |
| C | C, D/E |
| B | B, C, D/E |
| * | B*C, D/E |
| A | A, B*C, D/E |
| + | A+B*C, D/E |
| - | (A+B*C) - (D/E) ✓ |

---

#### (c) Conversion to Postfix (2 marks)

**Method:** Work from the innermost parentheses outward, replacing each sub-expression with its postfix equivalent.

1. Innermost: `(B * C)` → `B C *`
2. Innermost: `(D / E)` → `D E /`
3. Replace back: `(A + (B C *))` → `A B C * +`
4. Replace back: `((A B C * +) - (D E /))` → `A B C * + D E / -`

```
Postfix: A B C * + D E / -
```

**Verification (left-to-right scan, push operands; on operator, pop two and apply):**

| Read | Action | Stack |
|------|--------|-------|
| A | push | A |
| B | push | A, B |
| C | push | A, B, C |
| * | pop C,B → B*C | A, B*C |
| + | pop B*C,A → A+B*C | A+B*C |
| D | push | A+B*C, D |
| E | push | A+B*C, D, E |
| / | pop E,D → D/E | A+B*C, D/E |
| - | pop D/E, A+B*C → (A+B*C)-(D/E) | Result ✓ |

---

*End of Practice Test*
