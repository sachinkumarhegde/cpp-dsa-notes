# Area of a Circle

## Formula

```text
Area = π × r²
```

where `r` is the radius.

## C++ Program

```cpp
class Solution {
public:
    double areaOfCircle(double radius) {

        // Use acos(-1.0) to obtain a high-precision value of π.
        const double PI = acos(-1.0);

        return PI * radius * radius;
    }
};
```

## Example

For radius `5`:

```text
Area = π × 5²
     ≈ 78.54
```

## Complexity

- Time: `O(1)`
- Space: `O(1)`
