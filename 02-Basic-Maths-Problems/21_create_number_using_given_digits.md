# Create a Number Using Given Digits

## Problem

Given digits in an array, construct a number by placing them in the given order.

Example:

```text
digits = {1, 2, 3, 4}

Answer = 1234
```

## Core Pattern

Whenever a number must be constructed digit-by-digit:

```cpp
number = number * 10 + digit;
```

## C++ Program

```cpp
#include <vector>

class Solution {
public:
    long long createNumber(const std::vector<int>& digits) {

        long long number = 0;

        for (int digit : digits) {

            // Shift all existing digits one place to the left
            // and append the current digit.
            //
            // Example:
            // number = 123
            // digit  = 4
            // result = 123 * 10 + 4 = 1234
            number = number * 10 + digit;
        }

        return number;
    }
};
```

## Example

```text
{5, 8, 2}

5
58
582
```

Answer:

```text
582
```

## Important Edge Case

If the input contains leading zeroes:

```text
{0, 1, 2}
```

the integer result is:

```text
12
```

because integers do not preserve leading zeroes.

## Complexity

If there are `N` digits:

- Time: `O(N)`
- Space: `O(1)`
