# Count Total Set Bits in a Number

## Problem

Count the number of `1` bits in the binary representation of a number.

Example:

```text
13 = 1101

Set bits = 3
```

## Method 1 — Check Every Bit

```cpp
class Solution {
public:
    int countSetBits(unsigned int num) {

        int count = 0;

        while (num != 0) {

            // Check the least significant bit.
            count += (num & 1);

            // Shift all bits one position to the right.
            num >>= 1;
        }

        return count;
    }
};
```

Complexity:

- Time: `O(log N)` for a value of `N`
- Space: `O(1)`

## Method 2 — Brian Kernighan's Algorithm

Key operation:

```cpp
num = num & (num - 1);
```

It removes the lowest set bit.

```cpp
class Solution {
public:
    int countSetBits(unsigned int num) {

        int count = 0;

        while (num != 0) {

            // Each iteration removes one set bit.
            num = num & (num - 1);

            count++;
        }

        return count;
    }
};
```

Complexity:

- Time: `O(K)`, where `K` is the number of set bits
- Space: `O(1)`

## Interview Recommendation

Know both methods.

For an interview, remember:

```cpp
n = n & (n - 1);
```

means:

> Remove the lowest set bit.
