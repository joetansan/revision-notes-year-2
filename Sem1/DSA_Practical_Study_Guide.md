# 📚 DSA Practical Test — Study Guide (Topics 6–10)

> **Quick-reference revision guide for IT2X11 Data Structures & Algorithms**
> Covers: Advanced Sorting, Array-based Sequences, Stacks, Queues, Singly Linked Lists

---

## Table of Contents

1. [Topic 6: Advanced Sorting — Merge Sort & Quick Sort](#topic-6-advanced-sorting--merge-sort--quick-sort)
2. [Topic 7: Array-based Sequences](#topic-7-array-based-sequences)
3. [Topic 8: Stacks](#topic-8-stacks)
4. [Topic 9: Queues](#topic-9-queues)
5. [Topic 10: Singly Linked Lists](#topic-10-singly-linked-lists)

---

# Topic 6: Advanced Sorting — Merge Sort & Quick Sort

## 6.1 Divide-and-Conquer Overview

Both Merge Sort and Quick Sort use the **divide-and-conquer** strategy:

| Step | Description |
|------|-------------|
| **Divide** | Split the problem into smaller subproblems |
| **Recur** | Solve each subproblem recursively |
| **Conquer** | Combine the subproblem solutions into the final answer |

> ⚠️ **Pitfall:** Don't confuse "recur" and "conquer". Recur = solve subproblems. Conquer = combine the results.

---

## 6.2 Merge Sort

### How It Works

1. **Divide:** Split the list into two equal halves
2. **Recur:** Recursively sort each half
3. **Conquer:** Merge the two sorted halves into one sorted list

### Key Insight
The actual **ordering happens during the merge step**, not during the splitting.

### Base Case
A list with **0 or 1 elements** is already sorted — return it immediately.

### Python Implementation

```python
# Main merge sort function — returns a NEW sorted list
def mergeSort(theList):
    # Base case
    if len(theList) <= 1:
        return theList

    # Divide
    mid = len(theList) // 2
    leftHalf = mergeSort(theList[:mid])
    rightHalf = mergeSort(theList[mid:])

    # Conquer (merge)
    return mergeSortedLists(leftHalf, rightHalf)
```

### The Merge Operation (Step-by-Step)

```python
def mergeSortedLists(leftList, rightList):
    a = 0  # pointer for left list
    b = 0  # pointer for right list
    newList = []

    # Compare elements from both lists
    while a < len(leftList) and b < len(rightList):
        if leftList[a] <= rightList[b]:    # <= keeps it STABLE
            newList.append(leftList[a])
            a += 1
        else:
            newList.append(rightList[b])
            b += 1

    # Copy remaining elements (only one of these loops runs)
    while a < len(leftList):
        newList.append(leftList[a])
        a += 1

    while b < len(rightList):
        newList.append(rightList[b])
        b += 1

    return newList
```

### Merge Trace Example

Merging `[10, 23]` and `[18, 51]`:

| Step | Compare | Value Added | newList | Pointer Update |
|------|---------|-------------|---------|----------------|
| 1 | 10 vs 18 | 10 | [10] | a → 1 |
| 2 | 23 vs 18 | 18 | [10, 18] | b → 1 |
| 3 | 23 vs 51 | 23 | [10, 18, 23] | a → 2 (exhausted) |
| 4 | Append remaining | 51 | [10, 18, 23, 51] | Done |

> ⚠️ **Pitfall:** Use `<=` (not `<`) when comparing in the merge step. This ensures **stability** — equal elements keep their original relative order (take from the left list first).

---

## 6.3 Quick Sort

### How It Works

1. **Divide:** Pick a **pivot**, partition elements into values < pivot, = pivot, and > pivot
2. **Recur:** Recursively sort the left and right partitions
3. **Conquer:** The sorted partitions are already in the right place — just combine

### Key Insight
Quick Sort works **in-place** — it modifies the original list directly. The actual ordering happens during **partitioning**.

### Base Case
A range with **0 or 1 elements** (`first >= last`) is already sorted.

### Python Implementation (Hoare-style Partition)

```python
def quickSort(theSeq):
    n = len(theSeq)
    recQuickSort(theSeq, 0, n - 1)

def recQuickSort(theSeq, first, last):
    # Base case
    if first >= last:
        return

    # Partition and get pivot position
    pos = partitionSeq(theSeq, first, last)

    # Recursively sort left and right partitions
    recQuickSort(theSeq, first, pos - 1)
    recQuickSort(theSeq, pos + 1, last)

def partitionSeq(theSeq, first, last):
    pivot = theSeq[first]       # pivot = first element
    left = first + 1            # scan rightward
    right = last                # scan leftward

    while left <= right:
        # Move left marker right until value >= pivot
        while left <= right and theSeq[left] < pivot:
            left += 1
        # Move right marker left until value <= pivot
        while left <= right and theSeq[right] > pivot:
            right -= 1

        # Swap if markers haven't crossed
        if left <= right:
            theSeq[left], theSeq[right] = theSeq[right], theSeq[left]
            left += 1
            right -= 1

    # Place pivot in its correct position
    theSeq[first], theSeq[right] = theSeq[right], pivot
    return right
```

### Partition Trace Example

Sorting `[7, 2, 9, 4, 3, 8, 6, 1]`, pivot = 7:

| Step | Left stops at | Right stops at | Action | List after |
|------|---------------|----------------|--------|------------|
| Initial | idx 1 (2) | idx 7 (1) | pivot=7 | [7, 2, 9, 4, 3, 8, 6, 1] |
| 1 | idx 2 (9) | idx 7 (1) | Swap 9, 1 | [7, 2, 1, 4, 3, 8, 6, 9] |
| 2 | idx 5 (8) | idx 6 (6) | Swap 8, 6 | [7, 2, 1, 4, 3, 6, 8, 9] |
| 3 | left=6 | right=5 | Crossed! Swap pivot 7 with right (idx 5) | [6, 2, 1, 4, 3, **7**, 8, 9] |

Pivot 7 is now at index 5 (its final sorted position).

> ⚠️ **Pitfall:** After the markers cross, swap the pivot with `right` (not `left`). The `right` marker indicates the pivot's final position.

---

## 6.4 Merge Sort vs Quick Sort — Comparison

| Feature | Merge Sort | Quick Sort |
|---------|-----------|------------|
| **Main idea** | Split into halves, sort, merge | Pick pivot, partition, sort each side |
| **Best case** | O(n log n) | O(n log n) |
| **Average case** | O(n log n) | O(n log n) |
| **Worst case** | O(n log n) | **O(n²)** (poor pivot) |
| **Extra memory** | O(n) for merging | O(log n) recursion stack |
| **Stable?** | ✅ Yes (if merge takes left first on ties) | ❌ Not generally |
| **In-place?** | ❌ No | ✅ Yes |
| **Performance** | Predictable regardless of input | Often faster in practice |

### When to Use Which?

| Scenario | Choose | Reason |
|----------|--------|--------|
| Need stability (preserve order of equal keys) | **Merge Sort** | Stable by design |
| Sorting a linked list | **Merge Sort** | Merging works well with linked lists |
| Guaranteed O(n log n) needed | **Merge Sort** | Consistent in all cases |
| Large in-memory dataset, speed is priority | **Quick Sort** | Fast in practice, low overhead |
| Memory is limited | **Quick Sort** | In-place sorting |
| Nearly sorted data | **Merge Sort** | Quick Sort can degrade with poor pivot |

> ⚠️ **Pitfall:** Quick Sort's worst case O(n²) happens when the pivot is always the smallest or largest value (e.g., already sorted list with first-element pivot). Random or median-of-three pivot strategies help avoid this.

---

# Topic 7: Array-based Sequences

## 7.1 Python List Operations — Quick Reference

| Operation | Method | Time Complexity | Description |
|-----------|--------|-----------------|-------------|
| Add to end | `append(item)` | **O(1)** amortized | Adds item at the end |
| Insert at index | `insert(i, item)` | **O(n)** | Shifts elements right |
| Remove by value | `remove(item)` | **O(n)** | Searches, then shifts |
| Remove by index | `pop(i)` | **O(n)** | Removes and returns item at index i |
| Remove last | `pop()` | **O(1)** | Removes and returns last item |
| Find index | `index(item)` | **O(n)** | Returns index of first occurrence |
| Get length | `len(lst)` | **O(1)** | Returns number of items |
| Access by index | `lst[i]` | **O(1)** | Direct access |

```python
# Examples
my_list = [2, 6, 8, 10, 50]

my_list.insert(1, 4)      # [2, 4, 6, 8, 10, 50]  — insert 4 at index 1
my_list.remove(50)         # [2, 4, 6, 8, 10]       — remove value 50
my_list.append(12)         # [2, 4, 6, 8, 10, 12]   — add 12 to end
my_list.reverse()          # [12, 10, 8, 6, 4, 2]   — reverse in-place
idx = my_list.index(10)    # 1                       — find index of 10
my_list[0] = 100           # [100, 10, 8, 6, 4, 2]  — update first element
my_list.sort()             # [2, 4, 6, 8, 10, 100]  — sort ascending
val = my_list.pop(2)       # removes element at index 2
```

> ⚠️ **Pitfall:** `remove()` removes by **value** (first occurrence). `pop()` removes by **index**. Don't confuse them!

---

## 7.2 In-place vs New List

**In-place modification** — changes the original list:
```python
my_list.sort()           # sorts in-place, returns None
my_list.append(5)        # modifies in-place
my_list.reverse()        # reverses in-place
```

**Creating a new list** — original is unchanged:
```python
new_list = sorted(my_list)   # returns a NEW sorted list
new_list = my_list[::-1]     # returns a NEW reversed list
new_list = my_list[:]        # shallow copy — new container, same elements
```

---

## 7.3 Dynamic Array Concept

Python lists are **dynamic arrays** that automatically resize when they run out of space.

### How It Works

1. Python allocates a fixed-size block of memory
2. When the list fills up, Python allocates a **larger block** (typically 2× the size)
3. All elements are **copied** to the new block
4. The new item is then appended

### Amortized O(1) Append

Most `append()` operations are O(1), but occasionally one is O(n) when resizing occurs. **On average** across many operations, each append is still O(1) — this is called **amortized** time complexity.

> ⚠️ **Pitfall:** `insert(0, item)` is always O(n) because all existing elements must shift right. Don't use it for frequent front-insertions — use `collections.deque` instead.

---

## 7.4 Referential Arrays & Aliasing

Python lists store **references** (memory addresses) to objects, not the objects themselves.

```python
list_a = [10, 20, 30]

# ALIAS — same list object, two names
list_b = list_a
list_a[0] = 99
print(list_b)   # [99, 20, 30]  ← affected!

# SHALLOW COPY — new list container, same element references
list_c = list_a[:]
list_c[1] = 88
print(list_a)   # [99, 20, 30]  ← NOT affected!

# Another shallow copy
list_d = list(list_a)
```

| Operation | Creates new container? | Changes affect original? |
|-----------|----------------------|-------------------------|
| `list_b = list_a` | ❌ No (alias) | ✅ Yes |
| `list_c = list_a[:]` | ✅ Yes (shallow copy) | ❌ No |
| `list_d = list(list_a)` | ✅ Yes (shallow copy) | ❌ No |

> ⚠️ **Pitfall:** `list_b = list_a` does NOT copy the list. Both variables point to the **same** list object. Modifying one modifies the other.

---

## 7.5 Element Swapping and Repositioning

### Swapping two elements
```python
theList[i], theList[j] = theList[j], theList[i]
```

### Shifting elements right (for insertion)
```python
# Shift elements from index j to the right
for k in range(n - 1, j, -1):
    theList[k] = theList[k - 1]
```

### Removing in-place without creating a new list (two-pointer)
```python
def remove_zeros_inplace(lst):
    write_ptr = 0
    for read_ptr in range(len(lst)):
        if lst[read_ptr] != 0:
            lst[write_ptr] = lst[read_ptr]
            write_ptr += 1
    # Clear leftover slots
    for i in range(write_ptr, len(lst)):
        lst[i] = None
```

---

# Topic 8: Stacks

## 8.1 Stack Fundamentals

A **stack** is a linear data structure that follows the **LIFO (Last-In, First-Out)** principle. Items are added and removed from the same end, called the **top**.

### Stack Operations

| Operation | Description | Effect on Stack |
|-----------|-------------|-----------------|
| `push(item)` | Add item to the top | Stack grows by 1 |
| `pop()` | Remove and return top item | Stack shrinks by 1 |
| `peek()` | Return top item without removing | No change |
| `isEmpty()` | Check if stack is empty | No change |
| `__len__()` | Return number of items | No change |

### Real-world examples
- Undo feature in text editors
- Browser back button
- Function call stack
- Expression evaluation

---

## 8.2 Implementing Stack with Python List

The **top of the stack** is at the **end of the list** (`index -1`).

```python
class Stack:
    def __init__(self):
        self._theItems = list()

    def isEmpty(self):
        return len(self._theItems) == 0

    def __len__(self):
        return len(self._theItems)

    def peek(self):
        assert not self.isEmpty(), "Cannot peek at an empty stack"
        return self._theItems[-1]

    def pop(self):
        assert not self.isEmpty(), "Cannot pop from an empty stack"
        return self._theItems.pop()

    def push(self, item):
        self._theItems.append(item)

    def __str__(self):
        return str(self._theItems)
```

### Stack ↔ List Mapping

| Stack Operation | Python List Method | What happens in the list |
|-----------------|-------------------|--------------------------|
| `push(item)` | `append(item)` | Item added to end of list |
| `pop()` | `pop()` | Last item removed and returned |
| `peek()` | `[-1]` | Return last item, don't remove |

> ⚠️ **Pitfall:** Always check `isEmpty()` before `pop()` or `peek()`. Popping from an empty stack raises an `AssertionError`.

---

## 8.3 Common Stack Applications

### 1. Reversing a Sequence

```python
def reverseItems(items):
    s = Stack()
    for item in items:
        s.push(item)

    result = []
    while not s.isEmpty():
        result.append(s.pop())
    return result
```

### 2. Balanced Parentheses Checker

```python
def isBalanced(expression):
    s = Stack()
    opening = '([{'
    matching_open = {')': '(', ']': '[', '}': '{'}

    for ch in expression:
        if ch in opening:
            s.push(ch)
        elif ch in matching_open:
            if s.isEmpty():
                return False
            if s.pop() != matching_open[ch]:
                return False

    return s.isEmpty()  # stack must be empty at the end
```

**How it works:**
- Push opening brackets onto the stack
- When a closing bracket is found, pop the stack and check if they match
- At the end, the stack must be empty (all brackets matched)

> ⚠️ **Pitfall:** If a closing bracket appears when the stack is empty (e.g., `)A + B(`), return `False` immediately. Don't try to pop an empty stack.

### 3. Postfix Expression Evaluation

```python
def evaluatePostfix(expression):
    tokens = expression.split()
    s = Stack()

    for token in tokens:
        if isNumber(token):
            s.push(parseNumber(token))
        elif token in ['+', '-', '*', '/', '^']:
            right = s.pop()    # pop RIGHT operand first
            left = s.pop()     # then LEFT operand
            result = applyOperator(token, left, right)
            s.push(result)

    if len(s) != 1:
        raise ValueError("Invalid postfix expression")

    return s.pop()
```

**Key rule:** Pop the **right operand first**, then the left operand. This matters for `-` and `/`.

**Example trace:** `5 2 3 * + 4 -`

| Token | Action | Stack |
|-------|--------|-------|
| 5 | Push 5 | [5] |
| 2 | Push 2 | [5, 2] |
| 3 | Push 3 | [5, 2, 3] |
| * | Pop 3, 2 → 2*3=6 → Push 6 | [5, 6] |
| + | Pop 6, 5 → 5+6=11 → Push 11 | [11] |
| 4 | Push 4 | [11, 4] |
| - | Pop 4, 11 → 11-4=7 → Push 7 | [7] |

**Result: 7**

### 4. Infix to Postfix Conversion (4-step method)

For `A * (B + C) / D`:
1. Add parentheses: `((A * (B + C)) / D)`
2. Move operators after their operands: `((A (B C +) *) D /)`
3. Remove parentheses: `A B C + * D /`

> ⚠️ **Pitfall:** In postfix, operator precedence is encoded in the token order itself — no parentheses needed during evaluation.

---

# Topic 9: Queues

## 9.1 Queue Fundamentals

A **queue** is a linear data structure that follows the **FIFO (First-In, First-Out)** principle. Items are added at the **back** and removed from the **front**.

### Queue Operations

| Operation | Description | Effect on Queue |
|-----------|-------------|-----------------|
| `enqueue(item)` | Add item to the back | Queue grows by 1 |
| `dequeue()` | Remove and return front item | Queue shrinks by 1 |
| `peek()` | Return front item without removing | No change |
| `isEmpty()` | Check if queue is empty | No change |
| `__len__()` | Return number of items | No change |

### Real-world examples
- Print job scheduling
- Task scheduling in OS
- Web server request handling
- Breadth-first search (BFS)

---

## 9.2 Stack vs Queue — Key Differences

| Feature | Stack | Queue |
|---------|-------|-------|
| Principle | **LIFO** (Last-In, First-Out) | **FIFO** (First-In, First-Out) |
| Add item | `push` at **top** | `enqueue` at **back** |
| Remove item | `pop` from **top** | `dequeue` from **front** |
| Use when | Undo, backtracking, expressions | Scheduling, fair ordering |

---

## 9.3 Implementing Queue with Python List

```python
class Queue:
    def __init__(self):
        self._qList = list()

    def isEmpty(self):
        return len(self._qList) == 0

    def __len__(self):
        return len(self._qList)

    def enqueue(self, item):
        self._qList.append(item)       # add to back

    def dequeue(self):
        assert not self.isEmpty(), "Cannot dequeue from an empty queue."
        return self._qList.pop(0)      # remove from front

    def peek(self):
        assert not self.isEmpty(), "Cannot peek at an empty queue."
        return self._qList[0]

    def __str__(self):
        return ' '.join(str(item) for item in self._qList)
```

### Queue ↔ List Mapping

| Queue Operation | Python List Method | Position |
|-----------------|-------------------|----------|
| `enqueue(item)` | `append(item)` | Back (end of list) |
| `dequeue()` | `pop(0)` | Front (index 0) |
| `peek()` | `[0]` | Front (index 0) |

> ⚠️ **Pitfall:** `pop(0)` is **O(n)** because all remaining elements must shift forward. This makes the list-based queue inefficient for large queues. Use `collections.deque` for O(1) dequeue in real code.

---

## 9.4 Circular Array Queue

A **circular array** treats the array ends as connected, allowing pointers to **wrap around** using modulo arithmetic.

### Why Circular?
- `pop(0)` on a list is O(n) — shifting elements is wasteful
- With front/back pointers, no shifting is needed — both enqueue and dequeue become **O(1)**

### Key Components

| Component | Purpose |
|-----------|---------|
| `_qArray` | Fixed-size array to store items |
| `_front` | Index of the first item |
| `_back` | Index where the next item will be added |
| `_count` | Number of items currently in the queue |

### Implementation

```python
class Queue:
    def __init__(self, maxSize):
        self._count = 0
        self._front = 0
        self._back = maxSize - 1
        self._qArray = [None] * maxSize

    def isEmpty(self):
        return self._count == 0

    def isFull(self):
        return self._count == len(self._qArray)

    def __len__(self):
        return self._count

    def enqueue(self, item):
        assert not self.isFull(), "Cannot enqueue to a full queue."
        maxSize = len(self._qArray)
        self._back = (self._back + 1) % maxSize   # wrap around
        self._qArray[self._back] = item
        self._count += 1

    def dequeue(self):
        assert not self.isEmpty(), "Cannot dequeue from an empty queue."
        item = self._qArray[self._front]
        self._qArray[self._front] = None
        maxSize = len(self._qArray)
        self._front = (self._front + 1) % maxSize  # wrap around
        self._count -= 1
        return item

    def peek(self):
        assert not self.isEmpty(), "Cannot peek at an empty queue."
        return self._qArray[self._front]
```

### Wrap-around Formula

```python
next_index = (current_index + 1) % maxSize
```

### Trace Example (capacity 6)

| Step | Operation | front | back | count | Array [0..5] |
|------|-----------|-------|------|-------|--------------|
| 0 | Start | 0 | 5 | 0 | [None, None, None, None, None, None] |
| 1 | enqueue(10) | 0 | 0 | 1 | [10, None, None, None, None, None] |
| 2 | enqueue(20) | 0 | 1 | 2 | [10, 20, None, None, None, None] |
| 3 | enqueue(30) | 0 | 2 | 3 | [10, 20, 30, None, None, None] |
| 4 | dequeue()→10 | 1 | 2 | 2 | [None, 20, 30, None, None, None] |
| 5 | enqueue(40) | 1 | 3 | 3 | [None, 20, 30, 40, None, None] |
| 6 | enqueue(50) | 1 | 4 | 4 | [None, 20, 30, 40, 50, None] |
| 7 | enqueue(60) | 1 | 5 | 5 | [None, 20, 30, 40, 50, 60] |
| 8 | enqueue(70) | 2 | 0 | 5 | [70, None, 30, 40, 50, 60] |

At step 8: `back = (5 + 1) % 6 = 0` — wraps around to index 0!

> ⚠️ **Pitfall:** Distinguishing full vs empty is tricky when front == back. Use a **count** variable to avoid ambiguity. Empty: `count == 0`. Full: `count == maxSize`.

---

## 9.5 Queue Comparison Summary

| Implementation | Enqueue | Dequeue | Notes |
|---------------|---------|---------|-------|
| Python list | O(1) | **O(n)** | Simple but slow dequeue |
| Circular array | O(1) | O(1) | Fixed size, wrap-around |
| Linked list (head+tail) | O(1) | O(1) | Dynamic size |

---

# Topic 10: Singly Linked Lists

## 10.1 Node Structure

A **singly linked list** is made of **nodes**. Each node has:
- **data**: the value stored
- **next**: reference (pointer) to the next node, or `None` if it's the last node

```python
class ListNode:
    def __init__(self, data):
        self.data = data
        self.next = None
```

### Key Terms

| Term | Definition |
|------|-----------|
| **Node** | A storage object containing data and a next reference |
| **Head** | External reference to the first node; `None` if list is empty |
| **Tail** | External reference to the last node (optional optimization) |
| **Traversal** | Following next references from head to None |

> ⚠️ **Pitfall:** Unlike arrays/lists, linked lists **cannot** access an element by index directly. You must traverse from the head — this is O(n).

---

## 10.2 Traversal

```python
# Print all values
curNode = self._head
while curNode is not None:
    print(curNode.data)
    curNode = curNode.next
```

### String representation
```python
def __str__(self):
    values = []
    curNode = self._head
    while curNode is not None:
        values.append(str(curNode.data))
        curNode = curNode.next
    return " -> ".join(values) + " -> None"
```

---

## 10.3 Insert at Head (addFirst)

**O(1)** — just update a fixed number of references.

```python
def addFirst(self, data):
    newNode = ListNode(data)
    newNode.next = self._head    # point new node to current head
    self._head = newNode         # update head to new node
    self._size += 1
```

### Reference update order:
1. Set `newNode.next = self._head` (before changing head!)
2. Set `self._head = newNode`

> ⚠️ **Pitfall:** If you update `self._head` BEFORE setting `newNode.next`, you lose the reference to the rest of the list!

---

## 10.4 Insert at Tail (append)

**O(n)** with head only (must traverse to end).
**O(1)** with head AND tail references.

```python
# With head AND tail references
def append(self, data):
    newNode = ListNode(data)
    if self.isEmpty():
        self._head = newNode
    else:
        self._tail.next = newNode
    self._tail = newNode
    self._size += 1
```

---

## 10.5 Insert at Position (insertAt)

```python
def insertAt(self, index, data):
    assert 0 <= index <= self._size, "Invalid insertion index."

    if index == 0:
        self.addFirst(data)
        return

    # Find the node just before the insertion point
    predNode = self._head
    for _ in range(index - 1):
        predNode = predNode.next

    # Link new node
    newNode = ListNode(data)
    newNode.next = predNode.next    # point to what was at index
    predNode.next = newNode         # predecessor points to new node
    self._size += 1
```

### Reference update order for insertion at position:
1. `newNode.next = predNode.next` (before breaking the old link!)
2. `predNode.next = newNode`

> ⚠️ **Pitfall:** If you set `predNode.next = newNode` FIRST, you lose the reference to the rest of the list. Always set the new node's `next` first.

---

## 10.6 Remove First (removeFirst)

**O(1)** — just move head forward.

```python
def removeFirst(self):
    assert not self.isEmpty(), "Cannot remove from an empty linked list."
    tempNode = self._head
    self._head = self._head.next    # move head to second node
    tempNode.next = None            # detach removed node
    self._size -= 1
    return tempNode
```

> ⚠️ **Pitfall:** Always set `tempNode.next = None` after removal to cleanly detach the node and prevent accidental traversal into the old chain.

---

## 10.7 Remove by Value (removeNode)

```python
def removeNode(self, target):
    assert not self.isEmpty(), "Cannot remove from an empty linked list."

    predNode = None
    curNode = self._head

    # Search for target while tracking predecessor
    while curNode is not None and curNode.data != target:
        predNode = curNode
        curNode = curNode.next

    # Target not found
    if curNode is None:
        return None

    # Unlink the node
    if curNode is self._head:
        self._head = curNode.next       # removing head
    else:
        predNode.next = curNode.next    # skip over current node

    curNode.next = None                 # detach
    self._size -= 1
    return curNode
```

### Key points:
- Track both `predNode` (predecessor) and `curNode` (current)
- Special case: removing the head node (no predecessor)
- General case: `predNode.next = curNode.next` to skip over the removed node

> ⚠️ **Pitfall:** Forgetting to handle the case where the removed node is the **head** (predNode is None). The code must check `if curNode is self._head`.

---

## 10.8 Find a Node

```python
def find(self, target):
    curNode = self._head
    while curNode is not None:
        if curNode.data == target:
            return curNode
        curNode = curNode.next
    return None
```

---

## 10.9 Recursive Count

```python
def getCountRecursive(self):
    def countFrom(node):
        if node is None:
            return 0
        return 1 + countFrom(node.next)

    return countFrom(self._head)
```

> ⚠️ **Pitfall:** Recursive counting uses O(n) call-stack space. For very long lists, you may hit Python's recursion limit. Use an iterative approach for production code.

---

## 10.10 Head-and-Tail Linked List

Adding a **tail reference** makes appending O(1) instead of O(n).

```python
class HeadTailLinkedList:
    def __init__(self):
        self._head = None
        self._tail = None
        self._size = 0

    def isEmpty(self):
        return self._head is None

    def __len__(self):
        return self._size

    def append(self, data):
        newNode = ListNode(data)
        if self.isEmpty():
            self._head = newNode
        else:
            self._tail.next = newNode
        self._tail = newNode
        self._size += 1

    def removeNode(self, target):
        predNode = None
        curNode = self._head

        while curNode is not None and curNode.data != target:
            predNode = curNode
            curNode = curNode.next

        if curNode is None:
            return None

        if curNode is self._head:
            self._head = curNode.next
        else:
            predNode.next = curNode.next

        # Update tail if we removed the last node
        if curNode is self._tail:
            self._tail = predNode

        curNode.next = None
        self._size -= 1

        # If list is now empty, reset tail too
        if self._head is None:
            self._tail = None

        return curNode
```

### When removing a node with tail reference:
- If the removed node IS the tail → set `self._tail = predNode`
- If the list becomes empty → set both `self._head = None` AND `self._tail = None`

> ⚠️ **Pitfall:** When removing the last node, you must update BOTH head and tail to `None`. Forgetting to update tail causes it to point to a removed (orphaned) node.

---

## 10.11 Complexity Summary

| Operation | Head Only | Head + Tail | Why? |
|-----------|-----------|-------------|------|
| `addFirst(data)` | O(1) | O(1) | Only head references change |
| `append(data)` | **O(n)** | **O(1)** | Tail gives direct access to end |
| `removeFirst()` | O(1) | O(1) | Head moves to second node |
| `find(target)` | O(n) | O(n) | Must traverse from head |
| `removeNode(target)` | O(n) | O(n) | Must find the node first |
| `insertAt(0, data)` | O(1) | O(1) | Reuses addFirst |
| `insertAt(n, data)` | O(n) | O(n) | Must traverse to position |

---

## 10.12 Extending a LinkedList Class

To add a new method, follow this pattern:

1. **Identify the operation** (search, insert, modify, etc.)
2. **Use traversal** — start at `self._head`, follow `next` references
3. **Handle edge cases** — empty list, single node, head/tail changes
4. **Update `_size`** if adding/removing nodes

### Example: Move a node to the front

```python
def moveToFront(self, target):
    predNode = None
    curNode = self._head

    # Find target
    while curNode is not None and curNode.data != target:
        predNode = curNode
        curNode = curNode.next

    if curNode is None:
        return False         # not found

    if curNode is self._head:
        return True          # already at front

    # Unlink from current position
    predNode.next = curNode.next

    # Update tail if we moved the last node
    if curNode is self._tail:
        self._tail = predNode

    # Link before current head
    curNode.next = self._head
    self._head = curNode
    return True
```

---

# Quick Reference: Common Patterns

## Pattern 1: Traverse and process each node
```python
curNode = self._head
while curNode is not None:
    # process curNode.data
    curNode = curNode.next
```

## Pattern 2: Find node with predecessor
```python
predNode = None
curNode = self._head
while curNode is not None and curNode.data != target:
    predNode = curNode
    curNode = curNode.next
```

## Pattern 3: Stack-based bracket matching
```python
for ch in expression:
    if ch in opening: s.push(ch)
    elif ch in closing:
        if s.isEmpty(): return False
        if s.pop() != matching[ch]: return False
return s.isEmpty()
```

## Pattern 4: Postfix evaluation with stack
```python
for token in tokens:
    if is_number(token): s.push(token)
    else:
        right, left = s.pop(), s.pop()
        s.push(apply(token, left, right))
return s.pop()
```

## Pattern 5: Circular array wrap-around
```python
next_pos = (current_pos + 1) % array_size
```

---

# ⚠️ Common Pitfalls — Master List

| Topic | Pitfall |
|-------|---------|
| Merge Sort | Using `<` instead of `<=` in merge — breaks stability |
| Merge Sort | Forgetting to append remaining elements after main loop |
| Quick Sort | Swapping pivot with `left` instead of `right` after markers cross |
| Quick Sort | O(n²) worst case with poor pivot (already sorted data) |
| Lists | `remove(item)` removes by VALUE, `pop(i)` removes by INDEX |
| Lists | `list_b = list_a` creates an alias, NOT a copy |
| Lists | `insert(0, item)` is O(n) — avoid for frequent front-insertions |
| Stacks | Popping/peeking an empty stack → always check `isEmpty()` first |
| Stacks | In postfix eval, pop RIGHT operand first, then LEFT |
| Queues | `pop(0)` is O(n) — inefficient for large queues |
| Queues | Full vs empty ambiguity in circular queues — use a count variable |
| Queues | Forgetting to wrap around: use `(index + 1) % maxSize` |
| Linked Lists | Updating head BEFORE setting newNode.next → loses rest of list |
| Linked Lists | Not setting `removedNode.next = None` after removal |
| Linked Lists | Removing tail node without updating `self._tail` reference |
| Linked Lists | Removing last node must reset BOTH head and tail to `None` |
| Linked Lists | No index-based access — must traverse from head (O(n)) |

---

*Good luck on your test! 🎯*
