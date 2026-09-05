# Average of Array Elements

## Problem

Given an array of integers, calculate the average of all elements.

### Example

```text
Input:  [2, 4, 6, 8, 10]

Sum = 30
Count = 5

Average = 30 / 5 = 6
```

---

## Approach 1 — Easy / Basic

### Logic

1. Traverse the array.
2. Add every element to `sum`.
3. Divide `sum` by the number of elements.
4. Return the result.

### C++17

```cpp
double average(vector<int>& nums)
{
    int sum = 0;

    for (int i = 0; i < nums.size(); i++)
        sum += nums[i];

    return (double)sum / nums.size();
}
```

### Complexity

- **Time:** O(n)
- **Space:** O(1)

### Key Point

Use `double` for the result because the average may not be an integer.

```cpp
return (double)sum / nums.size();
```

Without the cast:

```cpp
sum / nums.size()
```

both operands are integers, so integer division is performed.

---

## Approach 2 — Optimized / Robust

The basic approach is already **O(n)**, which is optimal because every element must be examined to calculate the exact average.

The main improvement is to use a wider integer type for the sum to safely handle larger values.

### C++17

```cpp
double average(vector<int>& nums)
{
    long long sum = 0;

    for (int x : nums)
        sum += x;

    return static_cast<double>(sum) / nums.size();
}
```

### Complexity

- **Time:** O(n)
- **Space:** O(1)

---

## Why Is This Already Optimal?

To calculate an average, we need the sum of all elements.

Therefore, every element must be visited at least once.

```text
Lower bound = O(n)
```

So an **O(n)** solution is optimal.

There is no meaningful asymptotic improvement such as O(log n) because we cannot calculate the exact sum without considering all elements.

---

## Edge Cases

### One element

```text
[10]

Average = 10
```

### Negative values

```text
[1, -1, 1, -1]

Sum = 0
Average = 0
```

### Non-integer average

```text
[1, 2]

Average = 1.5
```

This is why the return type should be `double`.

---

## Interview Takeaway

For **average of array elements**:

```text
Average = Sum / Number of Elements
```

Pattern:

```text
Traverse → Calculate Sum → Divide by n
```

**Time:** O(n)  
**Space:** O(1)  
**Optimal:** Yes
