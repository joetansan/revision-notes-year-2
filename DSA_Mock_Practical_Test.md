# IT2111/IT2211/IT2511 — Data Structures & Algorithms
# AY2026/27 S1
# Mock Practical Test

---

## Instructions

| Item | Detail |
|---|---|
| **Duration** | 1 hour 30 minutes |
| **Total marks** | 35 |
| **Questions** | 4 |
| **Format** | Open-book (you may refer to your practical solutions) |
| **Language** | Python |
| **Mode** | Individual |

- Read each question carefully before coding.
- Write your answers in Python `.py` files as instructed.
- Include test code where requested.
- Edge cases (empty inputs, single elements, items not found) will be tested.

---

## Tips for the Test

> Based on advice from your instructor and past practical sessions.

1. **Read the existing code first.** Many questions give you partially written code. Understand the class structure, variable names, and conventions (e.g., `_theItems`, `_head`, `_size`) before filling in the blanks.
2. **Trace by hand before coding.** For sorting and linked list questions, draw diagrams or write out the state of the data structure at each step. This catches off-by-one errors early.
3. **Don't forget edge cases.** Always ask yourself: What if the list is empty? What if there's only one element? What if the item isn't found?
4. **Reuse existing methods.** If a class already has `addFirst()`, use it inside `insertAt()` instead of rewriting the logic. The practical solutions do this consistently.
5. **Assert statements are your friends.** The provided code uses `assert` to guard against invalid operations (e.g., popping from an empty stack). Don't remove them — they help you debug.
6. **Test as you go.** After completing each method, run a quick test before moving on. Partially working code earns more marks than unfinished code.
7. **Manage your time.** Spend roughly: Q1 (25 min), Q2 (25 min), Q3 (25 min), Q4 (15 min). Attempt all questions — partial marks are awarded.
8. **__str__ methods are already done.** Don't waste time rewriting them. Use `print(yourObject)` to inspect state.
9. **For sorting questions, check the comparison operators.** The direction of `<` vs `>` and `<=` vs `>=` determines ascending vs descending order and stability.
10. **For linked list questions, always update `_size`.** Forgetting to increment or decrement `_size` is a common mistake that breaks `__len__()` and any index-based checks.

---

## Question 1 — Stack (10 marks)

### Q1a. Complete the Stack class (4 marks)

The following Stack class is partially implemented. Complete the four methods marked `# TODO`.

```python
# stack.py
# Implementation of the Stack ADT using a Python list.

class Stack:
    # Creates an empty stack.
    def __init__(self):
        self._theItems = list()

    # Returns True if the stack is empty or False otherwise.
    def isEmpty(self):
        # TODO (1 mark)

    # Returns the number of items in the stack.
    def __len__(self):
        # TODO (1 mark)

    # Returns the top item on the stack without removing it.
    def peek(self):
        assert not self.isEmpty(), "Cannot peek at an empty stack"
        # TODO (1 mark)

    # Pushes an item onto the top of the stack.
    def push(self, item):
        # TODO (1 mark)

    # Removes and returns the top item on the stack.
    def pop(self):
        assert not self.isEmpty(), "Cannot pop from an empty stack"
        return self._theItems.pop()

    # Returns the stack contents as a string.
    def __str__(self):
        return str(self._theItems)
```

### Q1b. Use the Stack to check for palindromes (6 marks)

Write a function `isPalindrome(text)` that uses the Stack class above to determine whether a given string is a **palindrome** (reads the same forwards and backwards).

**Requirements:**
- Ignore case (uppercase and lowercase are treated the same).
- Ignore spaces and punctuation — only consider letters and digits.
- Use a Stack to reverse the filtered characters, then compare.

**Hint:** Push all filtered characters onto the stack, then pop them off to build the reversed string.

**Function signature:**

```python
from stack import Stack

def isPalindrome(text):
    # Your code here
    pass
```

**Marking scheme:**

| Component | Marks |
|---|---|
| Correctly filters text (removes spaces/punctuation, converts to lowercase) | 1 |
| Pushes all filtered characters onto the stack | 1 |
| Pops characters to build reversed string | 1 |
| Correctly compares original and reversed | 1 |
| Handles edge cases (empty string, single character) | 1 |
| Test code with at least 4 test cases | 1 |

**Test cases to verify:**

| Input | Expected Output |
|---|---|
| `"Racecar"` | `True` |
| `"A man, a plan, a canal: Panama"` | `True` |
| `"hello"` | `False` |
| `""` (empty string) | `True` |
| `"x"` | `True` |
| `"Was it a car or a cat I saw?"` | `True` |

<details>
<summary>Click to reveal solution — Q1a</summary>

```python
# stack.py
# Implementation of the Stack ADT using a Python list.

class Stack:
    # Creates an empty stack.
    def __init__(self):
        self._theItems = list()

    # Returns True if the stack is empty or False otherwise.
    def isEmpty(self):
        return len(self._theItems) == 0

    # Returns the number of items in the stack.
    def __len__(self):
        return len(self._theItems)

    # Returns the top item on the stack without removing it.
    def peek(self):
        assert not self.isEmpty(), "Cannot peek at an empty stack"
        return self._theItems[-1]

    # Pushes an item onto the top of the stack.
    def push(self, item):
        self._theItems.append(item)

    # Removes and returns the top item on the stack.
    def pop(self):
        assert not self.isEmpty(), "Cannot pop from an empty stack"
        return self._theItems.pop()

    # Returns the stack contents as a string.
    def __str__(self):
        return str(self._theItems)
```

</details>

<details>
<summary>Click to reveal solution — Q1b</summary>

```python
from stack import Stack

def isPalindrome(text):
    # Step 1: Filter — keep only letters and digits, convert to lowercase
    filtered = ""
    for ch in text:
        if ch.isalnum():
            filtered += ch.lower()

    # Step 2: Push all filtered characters onto a stack
    s = Stack()
    for ch in filtered:
        s.push(ch)

    # Step 3: Pop characters to build the reversed string
    reversed_text = ""
    while not s.isEmpty():
        reversed_text += s.pop()

    # Step 4: Compare
    return filtered == reversed_text


# Test code
if __name__ == "__main__":
    tests = [
        ("Racecar", True),
        ("A man, a plan, a canal: Panama", True),
        ("hello", False),
        ("", True),
        ("x", True),
        ("Was it a car or a cat I saw?", True),
    ]

    for text, expected in tests:
        result = isPalindrome(text)
        status = "PASS" if result == expected else "FAIL"
        print(f'{status}: isPalindrome("{text}") = {result}')
```

</details>

---

## Question 2 — Sorting (10 marks)

### Q2a. Complete the Merge Sort implementation (6 marks)

The Merge Sort code below has blanks. Fill in each blank to make it work correctly.

```python
def mergeSortedLists(leftList, rightList):
    """Merges two sorted lists into one sorted list."""
    a = 0
    b = 0
    newList = []

    while a < len(leftList) and b < len(rightList):
        if leftList[a] <= rightList[b]:
            newList.append(__________)       # Blank 1
            a = a + 1
        else:
            newList.append(__________)       # Blank 2
            b = b + 1

    while a < len(leftList):
        newList.append(__________)           # Blank 3
        a = a + 1

    while b < len(rightList):
        newList.append(__________)           # Blank 4
        b = b + 1

    return __________                        # Blank 5


def mergeSort(theList):
    """Returns a new list containing the elements of theList in ascending order."""
    if len(theList) <= __________:           # Blank 6
        return theList

    mid = len(theList) // 2
    leftHalf = mergeSort(theList[:mid])
    rightHalf = mergeSort(theList[mid:])

    return mergeSortedLists(__________, __________)  # Blanks 7, 8
```

**Marking scheme for Q2a:**

| Component | Marks |
|---|---|
| Blanks 1–2: Correct element from left/right list | 1 |
| Blanks 3–4: Correct cleanup loops | 1 |
| Blank 5: Returns `newList` | 1 |
| Blank 6: Base case `1` | 1 |
| Blanks 7–8: Correct recursive calls passed to merge | 1 |
| Test code verifying the sort works | 1 |

### Q2b. Counting comparisons during merge (4 marks)

Modify `mergeSortedLists` to create a new function `mergeSortedListsCount(leftList, rightList)` that **also returns the number of comparisons made** between elements during the merge.

Each time the function compares `leftList[a]` to `rightList[b]`, that counts as **one comparison**. Comparisons in the cleanup loops do **not** count.

Write the function, then use it to build `mergeSortCount(theList)` that returns **both** the sorted list **and** the total number of comparisons.

**Function signatures:**

```python
def mergeSortedListsCount(leftList, rightList):
    """Returns (mergedList, comparisons)"""
    pass

def mergeSortCount(theList):
    """Returns (sortedList, totalComparisons)"""
    pass
```

**Test cases to verify:**

```python
# Test Q2a
print(mergeSort([38, 12, 45, 7, 19]))
# Expected: [7, 12, 19, 38, 45]

print(mergeSort([]))
# Expected: []

print(mergeSort([5]))
# Expected: [5]

print(mergeSort([3, 3, 3]))
# Expected: [3, 3, 3]

# Test Q2b
sorted_list, count = mergeSortCount([38, 12, 45, 7, 19])
print(f"Sorted: {sorted_list}, Comparisons: {count}")
# Sorted: [7, 12, 19, 38, 45]
# Comparisons will vary — verify your count is consistent

sorted_list, count = mergeSortCount([1, 2, 3, 4, 5])
print(f"Sorted: {sorted_list}, Comparisons: {count}")
# An already-sorted list should make exactly 4 comparisons at the merge step

sorted_list, count = mergeSortCount([])
print(f"Sorted: {sorted_list}, Comparisons: {count}")
# Sorted: [], Comparisons: 0
```

<details>
<summary>Click to reveal solution — Q2a</summary>

```python
def mergeSortedLists(leftList, rightList):
    """Merges two sorted lists into one sorted list."""
    a = 0
    b = 0
    newList = []

    while a < len(leftList) and b < len(rightList):
        if leftList[a] <= rightList[b]:
            newList.append(leftList[a])       # Blank 1
            a = a + 1
        else:
            newList.append(rightList[b])      # Blank 2
            b = b + 1

    while a < len(leftList):
        newList.append(leftList[a])           # Blank 3
        a = a + 1

    while b < len(rightList):
        newList.append(rightList[b])          # Blank 4
        b = b + 1

    return newList                            # Blank 5


def mergeSort(theList):
    if len(theList) <= 1:                     # Blank 6
        return theList

    mid = len(theList) // 2
    leftHalf = mergeSort(theList[:mid])
    rightHalf = mergeSort(theList[mid:])

    return mergeSortedLists(leftHalf, rightHalf)  # Blanks 7, 8


# Test code
if __name__ == "__main__":
    print(mergeSort([38, 12, 45, 7, 19]))  # [7, 12, 19, 38, 45]
    print(mergeSort([]))                    # []
    print(mergeSort([5]))                   # [5]
    print(mergeSort([3, 3, 3]))             # [3, 3, 3]
```

</details>

<details>
<summary>Click to reveal solution — Q2b</summary>

```python
def mergeSortedListsCount(leftList, rightList):
    """Merges two sorted lists into one sorted list and counts comparisons."""
    a = 0
    b = 0
    newList = []
    comparisons = 0

    while a < len(leftList) and b < len(rightList):
        comparisons += 1                    # Count this comparison
        if leftList[a] <= rightList[b]:
            newList.append(leftList[a])
            a = a + 1
        else:
            newList.append(rightList[b])
            b = b + 1

    while a < len(leftList):
        newList.append(leftList[a])
        a = a + 1

    while b < len(rightList):
        newList.append(rightList[b])
        b = b + 1

    return newList, comparisons


def mergeSortCount(theList):
    """Returns (sortedList, totalComparisons)."""
    if len(theList) <= 1:
        return theList, 0

    mid = len(theList) // 2
    leftHalf, leftCount = mergeSortCount(theList[:mid])
    rightHalf, rightCount = mergeSortCount(theList[mid:])

    merged, mergeCount = mergeSortedListsCount(leftHalf, rightHalf)
    totalComparisons = leftCount + rightCount + mergeCount

    return merged, totalComparisons


# Test code
if __name__ == "__main__":
    sorted_list, count = mergeSortCount([38, 12, 45, 7, 19])
    print(f"Sorted: {sorted_list}, Comparisons: {count}")

    sorted_list, count = mergeSortCount([1, 2, 3, 4, 5])
    print(f"Sorted: {sorted_list}, Comparisons: {count}")

    sorted_list, count = mergeSortCount([])
    print(f"Sorted: {sorted_list}, Comparisons: {count}")
```

</details>

---

## Question 3 — Array-based Sequences (10 marks)

### Q3a. Remove duplicates from a sorted list in-place (6 marks)

Write a function `removeDuplicates(sortedList)` that removes duplicate values from a **sorted** list **in-place** (without creating a new list). After the function runs, each value should appear only once, and the function should return the new logical length of the list.

**Requirements:**
- Do **not** create a new list or use extra data structures.
- Use a **write pointer** approach: maintain a `write` index for where the next unique value should go, and a `read` index to scan through the list.
- After the function, the first `newLength` elements of the list contain the unique values in sorted order. The remaining elements at the end are irrelevant.

**Function signature:**

```python
def removeDuplicates(sortedList):
    """
    Removes duplicates from a sorted list in-place.
    Returns the new logical length of the list.
    """
    pass
```

**Test cases:**

| Input list (before) | New length | List state after (first `newLength` elements) |
|---|---|---|
| `[1, 1, 2, 3, 3, 3, 4]` | 4 | `[1, 2, 3, 4, ...]` |
| `[5, 5, 5, 5]` | 1 | `[5, ...]` |
| `[1, 2, 3]` | 3 | `[1, 2, 3]` |
| `[]` | 0 | `[]` |
| `[7]` | 1 | `[7]` |
| `[1, 1, 2, 2, 3, 3]` | 3 | `[1, 2, 3, ...]` |

**Marking scheme for Q3a:**

| Component | Marks |
|---|---|
| Correct use of write and read pointers | 2 |
| Correctly copies unique elements forward | 1 |
| Returns correct new length | 1 |
| Handles empty list edge case | 1 |
| Test code with at least 4 test cases | 1 |

### Q3b. Merge two sorted lists into one sorted list (4 marks)

Write a function `mergeTwoSorted(list1, list2)` that takes two **already sorted** Python lists and returns a **new** sorted list containing all elements from both.

**Requirements:**
- Do **not** use Python's built-in `sorted()` or `list.sort()`.
- Use the two-pointer merge technique (similar to the merge step in Merge Sort).
- Handle the case where one list is exhausted before the other.

**Function signature:**

```python
def mergeTwoSorted(list1, list2):
    """Returns a new sorted list containing all elements from list1 and list2."""
    pass
```

**Test cases:**

| list1 | list2 | Expected result |
|---|---|---|
| `[1, 3, 5]` | `[2, 4, 6]` | `[1, 2, 3, 4, 5, 6]` |
| `[1, 2, 3]` | `[]` | `[1, 2, 3]` |
| `[]` | `[4, 5, 6]` | `[4, 5, 6]` |
| `[]` | `[]` | `[]` |
| `[1, 1, 2]` | `[1, 3, 3]` | `[1, 1, 1, 2, 3, 3]` |
| `[10]` | `[5]` | `[5, 10]` |

**Marking scheme for Q3b:**

| Component | Marks |
|---|---|
| Correct two-pointer merge logic | 2 |
| Handles remaining elements from either list | 1 |
| Test code with at least 4 test cases | 1 |

<details>
<summary>Click to reveal solution — Q3a</summary>

```python
def removeDuplicates(sortedList):
    """
    Removes duplicates from a sorted list in-place.
    Returns the new logical length of the list.
    """
    if len(sortedList) == 0:
        return 0

    write = 0  # Position for the next unique element

    for read in range(1, len(sortedList)):
        if sortedList[read] != sortedList[write]:
            write += 1
            sortedList[write] = sortedList[read]

    return write + 1


# Test code
if __name__ == "__main__":
    # Test 1
    lst = [1, 1, 2, 3, 3, 3, 4]
    new_len = removeDuplicates(lst)
    print(f"New length: {new_len}, Elements: {lst[:new_len]}")
    # New length: 4, Elements: [1, 2, 3, 4]

    # Test 2
    lst = [5, 5, 5, 5]
    new_len = removeDuplicates(lst)
    print(f"New length: {new_len}, Elements: {lst[:new_len]}")
    # New length: 1, Elements: [5]

    # Test 3
    lst = [1, 2, 3]
    new_len = removeDuplicates(lst)
    print(f"New length: {new_len}, Elements: {lst[:new_len]}")
    # New length: 3, Elements: [1, 2, 3]

    # Test 4
    lst = []
    new_len = removeDuplicates(lst)
    print(f"New length: {new_len}, Elements: {lst[:new_len]}")
    # New length: 0, Elements: []

    # Test 5
    lst = [7]
    new_len = removeDuplicates(lst)
    print(f"New length: {new_len}, Elements: {lst[:new_len]}")
    # New length: 1, Elements: [7]

    # Test 6
    lst = [1, 1, 2, 2, 3, 3]
    new_len = removeDuplicates(lst)
    print(f"New length: {new_len}, Elements: {lst[:new_len]}")
    # New length: 3, Elements: [1, 2, 3]
```

</details>

<details>
<summary>Click to reveal solution — Q3b</summary>

```python
def mergeTwoSorted(list1, list2):
    """Returns a new sorted list containing all elements from list1 and list2."""
    result = []
    i = 0  # pointer for list1
    j = 0  # pointer for list2

    while i < len(list1) and j < len(list2):
        if list1[i] <= list2[j]:
            result.append(list1[i])
            i += 1
        else:
            result.append(list2[j])
            j += 1

    # Append remaining elements from list1
    while i < len(list1):
        result.append(list1[i])
        i += 1

    # Append remaining elements from list2
    while j < len(list2):
        result.append(list2[j])
        j += 1

    return result


# Test code
if __name__ == "__main__":
    print(mergeTwoSorted([1, 3, 5], [2, 4, 6]))  # [1, 2, 3, 4, 5, 6]
    print(mergeTwoSorted([1, 2, 3], []))           # [1, 2, 3]
    print(mergeTwoSorted([], [4, 5, 6]))            # [4, 5, 6]
    print(mergeTwoSorted([], []))                   # []
    print(mergeTwoSorted([1, 1, 2], [1, 3, 3]))    # [1, 1, 1, 2, 3, 3]
    print(mergeTwoSorted([10], [5]))                # [5, 10]
```

</details>

---

## Question 4 — Linked List (5 marks)

### Q4. Add a `countOccurrences` method to the Singly Linked List

The following `SinglyLinkedList` class is provided. Add a method `countOccurrences(target)` that returns the **number of nodes** whose `data` equals `target`.

```python
# singlylinkedlist.py

class ListNode:
    def __init__(self, data):
        self.data = data
        self.next = None


class SinglyLinkedList:
    def __init__(self):
        self._head = None
        self._size = 0

    def isEmpty(self):
        return self._head is None

    def __len__(self):
        return self._size

    def addFirst(self, data):
        newNode = ListNode(data)
        newNode.next = self._head
        self._head = newNode
        self._size += 1

    def __str__(self):
        values = []
        curNode = self._head
        while curNode is not None:
            values.append(str(curNode.data))
            curNode = curNode.next
        return " -> ".join(values) + (" -> None" if values else "Empty")

    # ========================================================
    # WRITE YOUR METHOD BELOW
    # ========================================================

    def countOccurrences(self, target):
        """
        Returns the number of nodes whose data equals target.
        Traverses the linked list from head to end.
        """
        # Your code here
        pass
```

**Test cases:**

```python
ll = SinglyLinkedList()
for value in [3, 5, 3, 7, 3, 5]:
    ll.addFirst(value)

print("List:", ll)                    # 5 -> 3 -> 7 -> 3 -> 5 -> 3 -> None
print("Count of 3:", ll.countOccurrences(3))   # Expected: 3
print("Count of 5:", ll.countOccurrences(5))   # Expected: 2
print("Count of 7:", ll.countOccurrences(7))   # Expected: 1
print("Count of 9:", ll.countOccurrences(9))   # Expected: 0

ll2 = SinglyLinkedList()
print("Count in empty list:", ll2.countOccurrences(1))  # Expected: 0
```

**Marking scheme:**

| Component | Marks |
|---|---|
| Correct traversal from `_head` to `None` | 1 |
| Compares each node's `data` to `target` | 1 |
| Returns correct count | 1 |
| Handles empty list (returns 0) | 1 |
| Test code with at least 3 test cases | 1 |

<details>
<summary>Click to reveal solution</summary>

```python
def countOccurrences(self, target):
    """
    Returns the number of nodes whose data equals target.
    Traverses the linked list from head to end.
    """
    count = 0
    curNode = self._head

    while curNode is not None:
        if curNode.data == target:
            count += 1
        curNode = curNode.next

    return count


# Test code
if __name__ == "__main__":
    ll = SinglyLinkedList()
    for value in [3, 5, 3, 7, 3, 5]:
        ll.addFirst(value)

    print("List:", ll)
    print("Count of 3:", ll.countOccurrences(3))   # 3
    print("Count of 5:", ll.countOccurrences(5))   # 2
    print("Count of 7:", ll.countOccurrences(7))   # 1
    print("Count of 9:", ll.countOccurrences(9))   # 0

    ll2 = SinglyLinkedList()
    print("Count in empty list:", ll2.countOccurrences(1))  # 0
```

</details>

---

## End of Mock Practical Test

**Total: 35 marks**

| Question | Topic | Marks |
|---|---|---|
| Q1a | Complete Stack class | 4 |
| Q1b | Palindrome checker using Stack | 6 |
| Q2a | Complete Merge Sort | 6 |
| Q2b | Counting comparisons during merge | 4 |
| Q3a | Remove duplicates in-place | 6 |
| Q3b | Merge two sorted lists | 4 |
| Q4 | Count occurrences in linked list | 5 |
| **Total** | | **35** |
