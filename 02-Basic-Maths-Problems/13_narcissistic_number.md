# Narcissistic Number

## Definition

A number is narcissistic (also called an Armstrong number) if the sum of its digits, each raised to the power of the number of digits, equals the original number.

Example:

```text
153

Number of digits = 3

1³ + 5³ + 3³
= 1 + 125 + 27
= 153
```

Therefore `153` is narcissistic.

## Approach

1. Count the number of digits.
2. Extract each digit.
3. Raise each digit to the digit count.
4. Add the results.
5. Compare with the original number.

## C++ Program

```cpp
#include <cmath>

class Solution {
public:
    bool isNarcissistic(int num) {

        if (num < 0) {
            return false;
        }

        int original = num;

        // Count digits.
        int digits = 0;
        int temp = num;

        // 0 has one digit.
        if (temp == 0) {
            digits = 1;
        }
        else {
            while (temp != 0) {
                digits++;
                temp /= 10;
            }
        }

        long long sum = 0;
        temp = num;

        while (temp != 0) {

            // Extract the last digit.
            int digit = temp % 10;

            // Add digit^number_of_digits.
            sum += static_cast<long long>(std::pow(digit, digits));

            // Remove the last digit.
            temp /= 10;
        }

        // For num = 0, the sum should be 0.
        return sum == original;
    }
};
```

## Complexity

If `D` is the number of digits:

- Time: `O(D)`
- Space: `O(1)`

## Interview Note

For strict integer arithmetic, implement integer exponentiation instead of relying on floating-point `pow()`.
