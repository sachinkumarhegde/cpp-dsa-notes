# Set the Kth Bit

## Problem

Set the `k`th bit of an integer to `1`.

Assume **0-based indexing**, so:

```text
bit 0 → rightmost bit
bit 1 → second bit
bit 2 → third bit
...
```

## Core Idea

Create a mask with only the `k`th bit set:

```cpp
1 << k
```

Then use bitwise OR:

```cpp
num | (1 << k)
```

OR with `1` forces the selected bit to become `1`.

## Example

Set bit `2` of:

```text
num = 8 = 1000
```

Mask:

```text
1 << 2 = 0100
```

OR:

```text
  1000
| 0100
------
  1100 = 12
```

## C++ Program

```cpp
class Solution {
public:
    int setKthBit(int num, int k) {

        // 1 << k creates a number whose kth bit is 1
        // and all other bits are 0.
        int mask = (1 << k);

        // OR guarantees that the kth bit becomes 1.
        // Other bits remain unchanged.
        return num | mask;
    }
};
```

## Complexity

- Time: `O(1)`
- Space: `O(1)`

## Related Bit Operations

```cpp
// Set kth bit
num | (1 << k)

// Clear kth bit
num & ~(1 << k)

// Toggle kth bit
num ^ (1 << k)

// Check kth bit
(num >> k) & 1
```
