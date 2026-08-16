# Convert Temperature Between Celsius and Fahrenheit

## Formulas

### Celsius → Fahrenheit

```text
F = (C × 9 / 5) + 32
```

### Fahrenheit → Celsius

```text
C = (F - 32) × 5 / 9
```

## C++ Program

```cpp
class Solution {
public:
    double celsiusToFahrenheit(double celsius) {

        // Use 9.0 and 5.0 so the calculation is performed
        // using floating-point arithmetic.
        return (celsius * 9.0 / 5.0) + 32.0;
    }

    double fahrenheitToCelsius(double fahrenheit) {

        return (fahrenheit - 32.0) * 5.0 / 9.0;
    }
};
```

## Example

```text
0°C   = 32°F
100°C = 212°F
32°F  = 0°C
```

## Complexity

- Time: `O(1)`
- Space: `O(1)`
