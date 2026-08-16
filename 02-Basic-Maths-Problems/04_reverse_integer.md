# Reverse an Integer

## Problem

Reverse the digits of an integer.

Example:

```text
1234 → 4321
```

## Core Idea

Extract the last digit and build the reversed number.

```cpp
digit = num % 10;
ans = ans * 10 + digit;
num = num / 10;
```

## Example

For `1234`:

```text
digit = 4
ans = 0 * 10 + 4 = 4

digit = 3
ans = 4 * 10 + 3 = 43

digit = 2
ans = 43 * 10 + 2 = 432

digit = 1
ans = 432 * 10 + 1 = 4321
```

## C++ Program

```cpp
class Solution {
public:
    int reverseNumber(int num) {

        int ans = 0;

        while (num != 0) {

            // Extract the last digit.
            int digit = num % 10;

            // Shift the existing digits left by one position
            // and place the new digit at the end.
            //
            // Example:
            // ans = 43, digit = 2
            // ans = 43 * 10 + 2 = 432
            ans = ans * 10 + digit;

            // Remove the last digit from num.
            num = num / 10;
        }

        return ans;
    }
};
```

## Most Important Formula

```cpp
ans = ans * 10 + digit;
```

Remember this whenever you need to construct a number digit-by-digit.

## Complexity

- Time: `O(log10(N))`
- Space: `O(1)`
