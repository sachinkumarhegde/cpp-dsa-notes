# Check Even or Odd Using Bitwise AND

## Problem

Determine whether an integer is even or odd.

## Core Idea

The least significant bit of a binary number tells us whether it is even or odd.

```text
Even → last bit is 0
Odd  → last bit is 1
```

Therefore:

```cpp
num & 1
```

gives:

```text
0 → Even
1 → Odd
```

## Example

For `2`:

```text
2 = 0010

  0010
& 0001
------
  0000  → Even
```

For `3`:

```text
3 = 0011

  0011
& 0001
------
  0001  → Odd
```

## C++ Program

```cpp
class Solution {
public:
    string checkEvenOdd(int num) {

        // & 1 checks the least significant bit.
        //
        // Result 1 → odd
        // Result 0 → even
        if (num & 1) {
            return "Odd";
        }
        else {
            return "Even";
        }
    }
};
```

## Alternative

The conventional approach is:

```cpp
if (num % 2 == 0)
    // Even
else
    // Odd
```

## Interview Point

Know both approaches:

```cpp
num % 2
```

and

```cpp
num & 1
```

The bitwise version is useful when discussing binary representation and bit manipulation.

## Complexity

- Time: `O(1)`
- Space: `O(1)`
