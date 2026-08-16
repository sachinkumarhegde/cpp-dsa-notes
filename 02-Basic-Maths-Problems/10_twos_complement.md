# 2's Complement of a Number

## Definition

2's complement is commonly used to represent negative integers in binary.

To find the 2's complement of a fixed-width binary number:

1. Invert every bit.
2. Add `1`.

Example using 8 bits:

```text
5       = 00000101
invert  = 11111010
add 1   = 11111011

Therefore -5 = 11111011
```

## C++ Program — Fixed Width

```cpp
#include <cstdint>

class Solution {
public:
    uint8_t twosComplement(uint8_t num) {

        // For an 8-bit value, ~ flips every bit.
        // Adding 1 produces the 2's complement.
        //
        // uint8_t keeps the result within 8 bits.
        return static_cast<uint8_t>(~num + 1);
    }
};
```

## Important

2's complement depends on the **bit width** being considered.

For example, the representation of `-5` differs between 8-bit, 16-bit and 32-bit representations.

## Bitwise Identity

For a fixed-width integer:

```cpp
~num + 1
```

is the standard expression for its 2's complement.

## Complexity

- Time: `O(1)`
- Space: `O(1)`
