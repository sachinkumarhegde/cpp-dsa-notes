# Multiply Every Array Element by 10

## Problem

Given an array of integers, return a new array where every element is multiplied by `10`.

### Example

```text
Input:  [1, 2, 3, 4, 5]
Output: [10, 20, 30, 40, 50]
```

---

## Approach 1 — Easy / Basic

### Logic

1. Create a new array/vector for the result.
2. Traverse the input array.
3. Multiply each element by `10`.
4. Store the result in the new array.
5. Return the result.

### C++17

```cpp
vector<int> multiplyBy10(vector<int>& nums)
{
    vector<int> result;

    for (int x : nums)
        result.push_back(x * 10);

    return result;
}
```

### Complexity

- **Time:** O(n)
- **Space:** O(n) — output array

---

## Approach 2 — Optimized / In-Place

If modifying the original array is allowed, we can avoid creating another array.

### Logic

Traverse the array and multiply each element by `10` directly.

### C++17

```cpp
vector<int> multiplyBy10(vector<int>& nums)
{
    for (int& x : nums)
        x *= 10;

    return nums;
}
```

### Complexity

- **Time:** O(n)
- **Extra Space:** O(1)

> The returned array is the same array that was passed as input.

---

## Easy vs Optimized

| Approach | Time | Extra Space | Modifies Input |
|---|---:|---:|---|
| New vector | O(n) | O(n) | No |
| In-place | O(n) | O(1) | Yes |

### Important

Both approaches take **O(n)** time because every element must be processed.

The optimized approach only reduces **extra space** from O(n) to O(1).

---

## Edge Cases

### Single element

```text
Input:  [7]
Output: [70]
```

### Zero

```text
Input:  [0]
Output: [0]
```

### Negative numbers

```text
Input:  [0, -1, -100]
Output: [0, -10, -1000]
```

### Empty array

If empty arrays are allowed:

```text
Input:  []
Output: []
```

---

## Interview Takeaway

This is a basic **array traversal / iteration** problem.

Pattern:

```text
Traverse → Transform each element → Store result
```

If a new array is required:

```text
O(n) extra space
```

If modifying the input is allowed:

```text
O(1) extra space
```
