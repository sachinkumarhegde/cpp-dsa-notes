# GCD of Two Numbers

## Definition

GCD (Greatest Common Divisor) is the largest number that divides both numbers.

Example:

```text
GCD(12, 18) = 6
```

## Euclidean Algorithm

Key identity:

```text
gcd(a, b) = gcd(b, a % b)
```

Continue until `b == 0`.

The remaining `a` is the GCD.

## Example

```text
gcd(48, 18)

48 % 18 = 12
18 % 12 = 6
12 % 6  = 0

GCD = 6
```

## C++ Program

```cpp
class Solution {
public:
    int gcd(int a, int b) {

        // Keep replacing (a, b) with (b, a % b).
        // When b becomes 0, a is the GCD.
        while (b != 0) {
            int remainder = a % b;
            a = b;
            b = remainder;
        }

        return a;
    }
};
```

## Complexity

- Time: `O(log(min(A, B)))`
- Space: `O(1)` for the iterative version

## Must Remember

```cpp
while (b != 0) {
    int r = a % b;
    a = b;
    b = r;
}
```
