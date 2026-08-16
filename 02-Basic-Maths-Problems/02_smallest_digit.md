# Smallest Digit

## Problem

Given a positive integer, find the smallest digit present in the number.

## Core Idea

Extract each digit and maintain the smallest value seen so far.

```cpp
digit = num % 10;
num = num / 10;
```

For the running minimum:

```cpp
smallest = min(smallest, digit);
```

## Example

For `58321`:

```text
Digits: 5, 8, 3, 2, 1
Smallest = 1
```

## C++ Program

```cpp
#include <climits>
#include <algorithm>

class Solution {
public:
    int smallestDigit(int num) {

        // Start with the largest possible integer.
        // The first digit will replace INT_MAX.
        int smallest = INT_MAX;

        while (num != 0) {

            // Extract the last digit.
            int digit = num % 10;

            // Keep the smaller value.
            smallest = std::min(smallest, digit);

            // Remove the last digit.
            num = num / 10;
        }

        return smallest;
    }
};
```

## Key Pattern

This is a **running minimum** problem.

```cpp
smallest = min(smallest, digit);
```

For maximum, the same idea becomes:

```cpp
largest = max(largest, digit);
```

## Complexity

- Time: `O(log10(N))`
- Space: `O(1)`
