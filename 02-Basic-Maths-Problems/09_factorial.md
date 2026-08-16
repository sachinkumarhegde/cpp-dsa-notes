# Factorial of a Number

## Definition

Factorial of `N` is:

```text
N! = N × (N-1) × (N-2) × ... × 1
```

Example:

```text
5! = 5 × 4 × 3 × 2 × 1 = 120
```

Special case:

```text
0! = 1
```

## C++ Program — Iterative

```cpp
class Solution {
public:
    long long factorial(int n) {

        // 0! is also 1, so initializing result to 1
        // handles both n = 0 and n > 0.
        long long result = 1;

        for (int i = 2; i <= n; i++) {
            result *= i;
        }

        return result;
    }
};
```

## Complexity

- Time: `O(N)`
- Space: `O(1)`

## Interview Note

Factorial grows extremely quickly. Even `long long` overflows for sufficiently large `N`.
