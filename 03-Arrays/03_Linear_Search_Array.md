# Linear Search in an Array

## Problem

Given an array of integers `nums` and an integer `target`, find the **first occurrence** of `target`.

- If `target` is found, return its index.
- If `target` is not found, return `-1`.

### Example

```text
Input:
nums = [4, 2, 7, 1, 9, 3]
target = 7

Output:
2
```

`7` is present at index `2`.

---

## Approach 1 — Easy / Basic

### Logic

1. Start from index `0`.
2. Compare every element with `target`.
3. If an element matches, immediately return its index.
4. If the loop finishes, return `-1`.

### C++17

```cpp
int linearSearch(vector<int>& nums, int target)
{
    for (int i = 0; i < nums.size(); i++)
    {
        if (nums[i] == target)
            return i;
    }

    return -1;
}
```

### Complexity

- **Time:** O(n)
- **Space:** O(1)

### Why return immediately?

The problem asks for the **first occurrence**.

Example:

```text
nums = [4, 7, 2, 7, 9]
target = 7
```

The first `7` is at index `1`, so return `1` immediately.

---

## Approach 2 — Optimized

For an **unsorted array**, linear search is already optimal in terms of worst-case time.

We may use STL `find()` for cleaner code.

### C++17

```cpp
int linearSearch(vector<int>& nums, int target)
{
    auto it = find(nums.begin(), nums.end(), target);

    if (it != nums.end())
        return it - nums.begin();

    return -1;
}
```

### Complexity

- **Time:** O(n)
- **Space:** O(1)

> `std::find()` performs a linear search internally.

---

## Why Can't We Do Better?

For an unsorted array, the target could be anywhere.

Example:

```text
[8, 4, 2, 9, 7]
             ↑
           target
```

In the worst case, we must check every element.

Therefore:

```text
Worst-case time = O(n)
```

So linear search is the optimal general approach for an **unsorted array**.

---

## Duplicate Elements

The solution returns the **first occurrence**.

```text
nums = [2, 5, 3, 5, 7]
target = 5
```

Output:

```text
1
```

Not `3`.

---

## Edge Cases

### Target at first position

```text
nums = [10, 20, 30]
target = 10

Output = 0
```

### Target at last position

```text
nums = [10, 20, 30]
target = 30

Output = 2
```

### Target not present

```text
nums = [10, 20, 30]
target = 5

Output = -1
```

### Single element

```text
nums = [7]
target = 7

Output = 0
```

---

## Linear Search vs Binary Search

| Condition | Technique |
|---|---|
| Unsorted array | Linear Search |
| Sorted array | Binary Search |
| Need first occurrence in unsorted array | Linear Search |
| Need faster search on sorted data | Binary Search |

### Key Point

> **Unsorted array + search for a value → Linear Search**

---

## Interview Takeaway

Pattern:

```text
Traverse → Compare → Return index if found → Otherwise -1
```

**Time:** O(n)  
**Space:** O(1)

For an unsorted array, **O(n) is optimal** in the worst case.
