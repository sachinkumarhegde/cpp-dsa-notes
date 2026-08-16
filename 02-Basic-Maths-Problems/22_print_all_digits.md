# Print All Digits of an Integer

## Problem

Print every digit of an integer.

There are two common interpretations:

1. Print digits from **right to left** using `% 10`.
2. Print digits from **left to right**, which is usually the expected human-readable order.

## Right-to-Left Approach

```cpp
void printDigits(int num) {

    while (num != 0) {

        // Extract and print the last digit.
        int digit = num % 10;
        std::cout << digit << ' ';

        // Remove the last digit.
        num /= 10;
    }
}
```

For:

```text
1234
```

output:

```text
4 3 2 1
```

## Left-to-Right Approach

A simple approach is to convert the number to a string.

```cpp
#include <iostream>
#include <string>

void printDigits(int num) {

    // Convert the integer to a string so digits can be
    // accessed naturally from left to right.
    std::string s = std::to_string(num);

    for (char c : s) {
        std::cout << c << ' ';
    }
}
```

For:

```text
1234
```

output:

```text
1 2 3 4
```

## Mathematical Approach — Without String

Find the highest power of 10 first, then extract digits from left to right.

```cpp
#include <iostream>

void printDigits(int num) {

    if (num == 0) {
        std::cout << 0;
        return;
    }

    int divisor = 1;

    // Find the highest power of 10 <= num.
    while (num / divisor >= 10) {
        divisor *= 10;
    }

    while (divisor != 0) {

        // Extract the current leftmost digit.
        int digit = num / divisor;
        std::cout << digit << ' ';

        // Remove the extracted digit.
        num %= divisor;

        // Move to the next digit position.
        divisor /= 10;
    }
}
```

## Complexity

For `D` digits:

- Time: `O(D)`
- Space: `O(1)`

## Interview Note

If the question specifically tests `% 10` and `/ 10`, use the mathematical approach and explain that the basic `% 10` pattern naturally processes digits from right to left.
