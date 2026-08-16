# LCM of Two Numbers

## Definition

LCM (Least Common Multiple) is the smallest positive number divisible by both numbers.

Example:

```text
LCM(4, 6) = 12
```

## Important Formula

For positive integers:

```text
LCM(a, b) = (a / GCD(a, b)) × b
```

Divide before multiplying to reduce overflow risk.

## C++ Program

```cpp
class Solution {
public:
    long long lcm(int a, int b) {

        // Find GCD using the Euclidean algorithm.
        int x = a;
        int y = b;

        while (y != 0) {
            int r = x % y;
            x = y;
            y = r;
        }

        int gcd = x;

        // Divide before multiplying to reduce overflow risk.
        return (static_cast<long long>(a) / gcd) * b;
    }
};
```

## Complexity

- Time: `O(log(min(A, B)))`
- Space: `O(1)`

## Must Remember

```cpp
LCM = (a / GCD) * b;
```
