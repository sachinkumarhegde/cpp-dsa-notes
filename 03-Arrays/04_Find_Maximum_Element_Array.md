# Find Maximum Element in an Array

## Problem

Given an array of integers, find and return the **maximum element** in the array.

### Example

```text
Input:  [1, 2, 3, 4, 5]
Output: 5
```

For negative values:

```text
Input:  [-1, -2, -3, -4, -5]
Output: -1
```

---

## Approach 1 — Easy / Basic

### Logic

1. Assume the first element is the maximum.
2. Traverse the remaining elements.
3. If the current element is greater than the current maximum, update it.
4. Return the maximum.

### C++17

```cpp
int findMaximum(vector<int>& nums)
{
    int maximum = nums[0];

    for (int i = 1; i < nums.size(); i++)
    {
        if (nums[i] > maximum)
            maximum = nums[i];
    }

    return maximum;
}
```

### Complexity

- **Time:** O(n)
- **Space:** O(1)

### Important

Do **not** initialize the maximum to `0`.

Incorrect for an all-negative array:

```cpp
int maximum = 0;
```

For:

```text
[-5, -2, -10]
```

this would incorrectly return `0`.

Instead, initialize with the first element:

```cpp
int maximum = nums[0];
```

---

## Approach 2 — Optimized / STL

C++ provides `max_element()` to find the largest element.

### C++17

```cpp
int findMaximum(vector<int>& nums)
{
    return *max_element(nums.begin(), nums.end());
}
```

### Complexity

- **Time:** O(n)
- **Space:** O(1)

> `max_element()` still needs to examine every element, so the time complexity cannot be better than O(n).

---

## Why Is O(n) Optimal?

To know the maximum, every element must be considered.

For example:

```text
[5, 8, 2, 100, 3]
```

Until we examine every element, we cannot know whether a larger value exists later.

Therefore:

```text
Minimum required work = O(n)
```

So the O(n) solution is optimal.

---

## Edge Cases

### Single element

```text
Input:  [7]
Output: 7
```

### All negative

```text
Input:  [-8, -3, -10]
Output: -3
```

### Duplicate maximum

```text
Input:  [5, 9, 2, 9, 4]
Output: 9
```

### All elements equal

```text
Input:  [4, 4, 4]
Output: 4
```

---

## Common Mistake

### Wrong

```cpp
int maximum = 0;
```

Fails when all elements are negative.

### Correct

```cpp
int maximum = nums[0];
```

---

## Interview Takeaway

Pattern:

```text
Initialize max → Traverse → Compare → Update max
```

**Time:** O(n)  
**Space:** O(1)  
**Optimal:** Yes

### Recognition

> **Find largest/smallest element → Single traversal is enough.**
