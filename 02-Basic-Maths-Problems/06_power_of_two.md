# Check if a Number is a Power of 2

## Problem

Determine whether a number can be written as:

```text
2^x
```

where `x` is a non-negative integer.

Examples:

```text
1, 2, 4, 8, 16, 32, ...
```

## Core Idea

A positive power of 2 has exactly **one set bit (`1`)** in its binary representation.

```text
1  = 0001
2  = 0010
4  = 0100
8  = 1000
16 = 10000
```

The important bit trick is:

```cpp
num & (num - 1)
```

For a power of 2, the result is `0`.

## Why Does It Work?

Example:

```text
num = 8

8     = 1000
8 - 1 = 0111

  1000
& 0111
------
  0000
```

For `6`:

```text
6     = 0110
6 - 1 = 0101

  0110
& 0101
------
  0100  → not zero
```

## C++ Program

```cpp
class Solution {
public:
    string isPowerOfTwo(int num) {

        // Power of 2 must be positive.
        // 0 and negative numbers are not powers of 2.
        if (num <= 0) {
            return "No";
        }

        // A power of 2 has exactly one set bit.
        //
        // n & (n - 1) removes the rightmost set bit.
        // If only one set bit existed, nothing remains.
        if ((num & (num - 1)) == 0) {
            return "Yes";
        }

        return "No";
    }
};
```

## Important

Always include:

```cpp
num > 0
```

Otherwise `0` can incorrectly pass the bitwise condition.

## Formula to Remember

```cpp
num > 0 && (num & (num - 1)) == 0
```

## Complexity

- Time: `O(1)`
- Space: `O(1)`
