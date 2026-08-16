# Check Prime Number — Optimized

## Problem

Determine whether a number is prime efficiently.

## Key Optimization

We do not need to check every number from `2` to `num - 1`.

We only need to check divisors up to:

```cpp
sqrt(num)
```

or equivalently:

```cpp
i * i <= num
```

## Why √N?

If:

```text
num = a × b
```

and both `a` and `b` were greater than `sqrt(num)`, their product would be greater than `num`.

Therefore, if a number has a factor, at least one factor must be `<= sqrt(num)`.

### Example

For `36`:

```text
1 × 36
2 × 18
3 × 12
4 × 9
6 × 6
```

Once we reach:

```text
sqrt(36) = 6
```

we have checked enough.

## C++ Program

```cpp
class Solution {
public:
    string isPrime(int num) {

        // Numbers <= 1 are not prime.
        if (num <= 1) {
            return "No";
        }

        // We only need to check divisors up to sqrt(num).
        //
        // i * i <= num is used instead of sqrt(num)
        // to avoid calling the sqrt function.
        for (int i = 2; i * i <= num; i++) {

            // If num is exactly divisible by i,
            // then num has a divisor other than 1 and itself.
            if (num % i == 0) {
                return "No";
            }
        }

        // No divisor was found.
        return "Yes";
    }
};
```

## Complexity

- Time: `O(sqrt(N))`
- Space: `O(1)`

## Interview Recommendation

Prefer this version in interviews:

```cpp
for (int i = 2; i * i <= num; i++)
```

It is significantly better than checking all the way to `num - 1`.
