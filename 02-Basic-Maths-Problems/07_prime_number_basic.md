# Check Prime Number — Basic

## Problem

Determine whether a number is prime.

A prime number:

- is greater than `1`
- has exactly two positive divisors: `1` and itself

Examples:

```text
2, 3, 5, 7, 11 → Prime
```

```text
1, 4, 6, 9, 15 → Not Prime
```

## Core Idea

Check whether any number from `2` to `num - 1` divides `num`.

If:

```cpp
num % i == 0
```

then `num` is not prime.

## C++ Program

```cpp
class Solution {
public:
    string isPrime(int num) {

        // 0 and 1 are not prime numbers.
        if (num <= 1) {
            return "No";
        }

        // Check every possible divisor from 2 to num - 1.
        for (int i = 2; i < num; i++) {

            // If remainder is 0, i divides num.
            // Therefore, num is not prime.
            if (num % i == 0) {
                return "No";
            }
        }

        // No divisor was found.
        // Therefore, num is prime.
        return "Yes";
    }
};
```

## Complexity

- Time: `O(N)`
- Space: `O(1)`

## Interview Note

This is the straightforward solution, but it can be optimized to `O(sqrt(N))`.
