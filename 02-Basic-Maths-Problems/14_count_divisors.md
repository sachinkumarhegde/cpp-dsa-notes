# Count Divisors of a Number

## Problem

Find the total number of positive divisors of `N`.

Example:

```text
N = 12

Divisors:
1, 2, 3, 4, 6, 12

Answer = 6
```

## Optimized Idea

Divisors occur in pairs:

```text
12 → (1, 12), (2, 6), (3, 4)
```

So only check up to `sqrt(N)`.

If:

```cpp
i * i == num
```

then `i` is paired with itself, so count it only once.

## C++ Program

```cpp
class Solution {
public:
    int countDivisors(int num) {

        if (num <= 0) {
            return 0;
        }

        int count = 0;

        // Check only up to sqrt(num).
        for (int i = 1; i * i <= num; i++) {

            if (num % i == 0) {

                // i is one divisor.
                count++;

                // num / i is its paired divisor.
                // If i == num / i, both are the same divisor,
                // so do not count it twice.
                if (i != num / i) {
                    count++;
                }
            }
        }

        return count;
    }
};
```

## Complexity

- Time: `O(√N)`
- Space: `O(1)`

## Key Pattern

```cpp
for (int i = 1; i * i <= n; i++)
```

Use divisor pairs to avoid checking all numbers up to `N`.
