# Reverse Integer with Overflow Handling

## Problem

Reverse a signed 32-bit integer.

If the reversed result goes outside the 32-bit signed integer range, return `0`.

```text
INT_MIN = -2147483648
INT_MAX =  2147483647
```

## Core Idea

The normal reverse operation is:

```cpp
ans = ans * 10 + digit;
```

But `ans * 10` itself can overflow.

Therefore, check before performing the multiplication.

## C++ Program

```cpp
#include <climits>

class Solution {
public:
    int reverse(int num) {

        int ans = 0;

        while (num != 0) {

            // Extract the last digit.
            int digit = num % 10;

            // Check positive overflow before:
            // ans = ans * 10 + digit
            if (ans > INT_MAX / 10 ||
                (ans == INT_MAX / 10 && digit > 7)) {
                return 0;
            }

            // Check negative overflow.
            if (ans < INT_MIN / 10 ||
                (ans == INT_MIN / 10 && digit < -8)) {
                return 0;
            }

            // Build the reversed number.
            ans = ans * 10 + digit;

            // Remove the last digit.
            num = num / 10;
        }

        return ans;
    }
};
```

## Interview Point

For simple digit-reversal questions, remember:

```cpp
digit = num % 10;
ans = ans * 10 + digit;
num = num / 10;
```

For a fixed-width integer problem, also think about **overflow**.

## Complexity

- Time: `O(log10(N))`
- Space: `O(1)`
