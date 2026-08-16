# Sum of Digits

## Problem

Given a non-negative integer, find the sum of all its digits.

## Core Idea

Process the number one digit at a time from right to left.

- `num % 10` → extracts the last digit
- `num / 10` → removes the last digit

Repeat until `num` becomes `0`.

## Example

For `1234`:

```text
1234 % 10 = 4
123  % 10 = 3
12   % 10 = 2
1    % 10 = 1

Sum = 4 + 3 + 2 + 1 = 10
```

## C++ Program

```cpp
class Solution {
public:
    int sumOfDigits(int num) {

        int sum = 0;

        // Process every digit from right to left.
        while (num != 0) {

            // % 10 extracts the last digit.
            int digit = num % 10;

            // Add the current digit to the answer.
            sum = sum + digit;

            // / 10 removes the last digit.
            num = num / 10;
        }

        return sum;
    }
};
```

## Pattern to Remember

```cpp
int digit = num % 10;
num = num / 10;
```

## Complexity

- Time: `O(log10(N))` — number of digits
- Space: `O(1)`
