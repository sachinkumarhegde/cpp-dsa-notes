# 00 — Interview Cheat Sheet: Number & Digit Manipulation

> Quick revision sheet — use this before an interview.  
> Goal: recall the pattern, not reread a textbook.

---

## 1. The Core Digit Pattern

Whenever a problem asks you to work with individual digits:

```cpp
while (num != 0) {
    int digit = num % 10;  // Extract last digit

    // Process digit here

    num = num / 10;        // Remove last digit
}
```

### Memorize

```text
num % 10  → GET last digit
num / 10  → REMOVE last digit
```

This is the foundation for:

- Sum of digits
- Product of digits
- Count digits
- Smallest/largest digit
- Count even/odd digits
- Reverse number
- Palindrome number
- Digit frequency
- Armstrong number
- Digit-based comparisons

---

# 2. Building a Number Digit-by-Digit

When constructing a new number from digits:

```cpp
ans = ans * 10 + digit;
```

### Why?

If:

```text
ans = 43
digit = 2
```

then:

```text
43 * 10 + 2 = 432
```

### Used for

- Reverse integer
- Constructing filtered digits
- Removing/rearranging digits
- Palindrome-related problems

### Memorize

```cpp
ans = ans * 10 + digit;
```

---

# 3. Sum of Digits

```cpp
int sum = 0;

while (num != 0) {
    int digit = num % 10;
    sum += digit;
    num /= 10;
}
```

Pattern:

```cpp
sum += digit;
```

Complexity:

```text
Time  : O(log₁₀ N)
Space : O(1)
```

---

# 4. Product of Digits

Initialize with `1`, not `0`.

```cpp
int product = 1;

while (num != 0) {
    int digit = num % 10;
    product *= digit;
    num /= 10;
}
```

Complexity:

```text
Time  : O(log₁₀ N)
Space : O(1)
```

---

# 5. Count Digits

```cpp
int count = 0;

while (num != 0) {
    count++;
    num /= 10;
}
```

Complexity:

```text
Time  : O(log₁₀ N)
Space : O(1)
```

### Edge case

For `num = 0`, the number has one digit.

```cpp
if (num == 0)
    return 1;
```

---

# 6. Smallest / Largest Digit

### Smallest

```cpp
int smallest = INT_MAX;

while (num != 0) {
    int digit = num % 10;
    smallest = min(smallest, digit);
    num /= 10;
}
```

### Largest

```cpp
int largest = INT_MIN;

while (num != 0) {
    int digit = num % 10;
    largest = max(largest, digit);
    num /= 10;
}
```

Pattern:

```cpp
minValue = min(minValue, current);
maxValue = max(maxValue, current);
```

Complexity:

```text
Time  : O(log₁₀ N)
Space : O(1)
```

---

# 7. Even / Odd

## Normal approach

```cpp
if (num % 2 == 0) {
    // Even
}
else {
    // Odd
}
```

## Bitwise approach

```cpp
if (num & 1) {
    // Odd
}
else {
    // Even
}
```

### Remember

```text
num & 1 == 0 → Even
num & 1 == 1 → Odd
```

Complexity:

```text
Time  : O(1)
Space : O(1)
```

---

# 8. Reverse an Integer

Core pattern:

```cpp
int ans = 0;

while (num != 0) {
    int digit = num % 10;
    ans = ans * 10 + digit;
    num /= 10;
}
```

### Must memorize

```cpp
digit = num % 10;
ans = ans * 10 + digit;
num = num / 10;
```

Complexity:

```text
Time  : O(log₁₀ N)
Space : O(1)
```

---

# 9. Reverse Integer — Overflow

For 32-bit signed integers:

```text
INT_MAX =  2147483647
INT_MIN = -2147483648
```

Before:

```cpp
ans = ans * 10 + digit;
```

check for overflow.

```cpp
if (ans > INT_MAX / 10 ||
    (ans == INT_MAX / 10 && digit > 7)) {
    return 0;
}

if (ans < INT_MIN / 10 ||
    (ans == INT_MIN / 10 && digit < -8)) {
    return 0;
}
```

### Interview point

Do not blindly write:

```cpp
ans = ans * 10 + digit;
```

when the problem explicitly has a fixed integer range.

---

# 10. Palindrome Number

A number is a palindrome if it reads the same forward and backward.

Examples:

```text
121  → Palindrome
1331 → Palindrome
123  → Not palindrome
```

### Approach

1. Store original number.
2. Reverse the number.
3. Compare original and reversed values.

```cpp
int original = num;
int reversed = 0;

while (num != 0) {
    int digit = num % 10;
    reversed = reversed * 10 + digit;
    num /= 10;
}

return original == reversed;
```

### Better interview point

If overflow can matter, use a wider integer type or avoid constructing the full reverse depending on the problem constraints.

Complexity:

```text
Time  : O(log₁₀ N)
Space : O(1)
```

---

# 11. Power of 2

A positive power of 2 has exactly one set bit.

```text
1  = 0001
2  = 0010
4  = 0100
8  = 1000
16 = 10000
```

Use:

```cpp
num > 0 && (num & (num - 1)) == 0
```

### Why?

`n - 1` changes the rightmost `1` to `0` and all bits after it to `1`.

Example:

```text
8     = 1000
8 - 1 = 0111

1000
0111
----
0000
```

For `6`:

```text
6     = 0110
5     = 0101

0110
0101
----
0100  → not zero
```

### Must memorize

```cpp
n > 0 && (n & (n - 1)) == 0
```

Complexity:

```text
Time  : O(1)
Space : O(1)
```

---

# 12. Prime Number

A prime number:

- is greater than `1`
- has exactly two positive divisors: `1` and itself

### Basic

```cpp
if (num <= 1)
    return false;

for (int i = 2; i < num; i++) {
    if (num % i == 0)
        return false;
}

return true;
```

Complexity:

```text
Time  : O(N)
Space : O(1)
```

---

# 13. Optimized Prime Check

Only check up to `sqrt(N)`.

```cpp
if (num <= 1)
    return false;

for (int i = 2; i * i <= num; i++) {
    if (num % i == 0)
        return false;
}

return true;
```

### Why √N?

If:

```text
N = a × b
```

then at least one of `a` or `b` must be `<= √N`.

So finding no divisor up to `√N` means there is no divisor at all.

Complexity:

```text
Time  : O(√N)
Space : O(1)
```

### Interview recommendation

Prefer the `O(√N)` version.

---

# 14. Common Number-Problem Patterns

| Problem | Main Pattern |
|---|---|
| Sum digits | `sum += digit` |
| Product digits | `product *= digit` |
| Count digits | `count++` |
| Smallest digit | `min(min, digit)` |
| Largest digit | `max(max, digit)` |
| Reverse | `ans = ans * 10 + digit` |
| Palindrome | Original == Reverse |
| Even/Odd | `num % 2` or `num & 1` |
| Power of 2 | `n & (n - 1)` |
| Prime | Check divisors up to `√N` |

---

# 15. The Universal Digit Template

When stuck on a digit problem, start here:

```cpp
while (num != 0) {

    int digit = num % 10;

    // What do I need to do with this digit?

    num /= 10;
}
```

Then decide what the accumulator should be:

```text
Need sum?        → sum
Need product?    → product
Need count?      → count
Need minimum?    → min
Need maximum?    → max
Need reverse?    → ans = ans * 10 + digit
Need frequency?  → frequency[digit]++
```

---

# 16. Digit Frequency

Digits are from `0` to `9`, so an array of size `10` is enough.

```cpp
int frequency[10] = {};

while (num != 0) {
    int digit = num % 10;
    frequency[digit]++;
    num /= 10;
}
```

For example, `122333`:

```text
0 → 0
1 → 1
2 → 2
3 → 3
...
```

### Pattern

```cpp
frequency[digit]++;
```

Complexity:

```text
Time  : O(log₁₀ N)
Space : O(1)
```

Although the array has size `10`, its size is constant.

---

# 17. Armstrong Number — Pattern

An Armstrong number is a number equal to the sum of its digits raised to the number of digits.

Example:

```text
153

1³ + 5³ + 3³
= 1 + 125 + 27
= 153
```

General pattern:

```cpp
original = num;
count = numberOfDigits(num);

sum = 0;

while (num != 0) {
    digit = num % 10;
    sum += pow(digit, count);
    num /= 10;
}

return sum == original;
```

### Interview caution

`pow()` returns a floating-point value. For integer problems, consider integer exponentiation if exact integer arithmetic matters.

---

# 18. Common Edge Cases

Before coding, check:

```text
0
1
negative numbers
single-digit numbers
numbers ending in 0
very large numbers
integer overflow
```

### Example: trailing zero

```text
1200 → reverse = 21
```

The zeros disappear naturally because integers do not store leading zeros.

---

# 19. Negative Numbers

For digit problems, clarify how negative numbers should be handled.

In C++:

```cpp
-123 % 10
```

produces:

```text
-3
```

So if the problem expects digit values `0–9`, you may need to work with the absolute value or handle the sign separately.

Do not blindly assume the input is positive unless the constraints say so.

---

# 20. Integer Division

For positive integers:

```cpp
123 / 10 = 12
```

The fractional part is discarded.

This is exactly why:

```cpp
num /= 10;
```

removes the last digit.

---

# 21. Complexity of Digit Problems

If `N` has `D` digits:

```text
D = O(log₁₀ N)
```

Therefore, processing every digit once gives:

```text
Time  : O(log N)
Space : O(1)
```

The base of the logarithm is usually omitted in Big-O:

```text
O(log N)
```

---

# 22. Important C++ Operators

| Operator | Meaning | Example |
|---|---|---|
| `%` | Remainder | `17 % 10 = 7` |
| `/` | Integer division | `17 / 10 = 1` |
| `&` | Bitwise AND | `6 & 1` |
| `|` | Bitwise OR | `6 | 1` |
| `^` | Bitwise XOR | `6 ^ 1` |
| `<<` | Left shift | `1 << 3 = 8` |
| `>>` | Right shift | `8 >> 2 = 2` |

---

# 23. Bitwise Patterns Worth Remembering

## Check odd

```cpp
n & 1
```

## Remove lowest set bit

```cpp
n = n & (n - 1);
```

## Check power of 2

```cpp
n > 0 && (n & (n - 1)) == 0
```

## Get ith bit

```cpp
(n >> i) & 1
```

## Set ith bit

```cpp
n = n | (1 << i);
```

## Clear ith bit

```cpp
n = n & ~(1 << i);
```

## Toggle ith bit

```cpp
n = n ^ (1 << i);
```

---

# 24. Interview Thinking Process

When you see a number problem:

### Step 1 — Identify what is being asked

```text
Digit?
Number?
Divisibility?
Prime?
Binary representation?
```

### Step 2 — Look for constraints

Ask:

```text
How large can N be?
Can N be negative?
Can the answer overflow?
```

### Step 3 — Choose the pattern

```text
Digit problem
    ↓
% 10 and / 10

Binary problem
    ↓
Bitwise operators

Prime problem
    ↓
Check up to √N

Power of 2
    ↓
n & (n - 1)
```

### Step 4 — Handle edge cases

Especially:

```text
0
1
negative
overflow
```

### Step 5 — State complexity

Always be ready to say:

```text
Time complexity = ...
Space complexity = ...
```

---

# 25. Most Important Things to Memorize

## Digit extraction

```cpp
int digit = num % 10;
```

## Remove digit

```cpp
num /= 10;
```

## Build number

```cpp
ans = ans * 10 + digit;
```

## Running minimum

```cpp
minimum = min(minimum, value);
```

## Running maximum

```cpp
maximum = max(maximum, value);
```

## Count

```cpp
count++;
```

## Frequency

```cpp
frequency[value]++;
```

## Odd

```cpp
num & 1
```

## Power of 2

```cpp
num > 0 && (num & (num - 1)) == 0
```

## Prime

```cpp
for (int i = 2; i * i <= num; i++)
```

---

# 26. 30-Second Revision

```text
NUMBER / DIGIT PROBLEMS
=======================

% 10       → last digit
/ 10       → remove last digit

sum += d   → sum
prod *= d  → product
count++    → count
min(...)   → minimum
max(...)   → maximum

ans*10+d   → construct/reverse number

original == reverse
           → palindrome

n & 1      → odd/even

n & (n-1)  → removes lowest set bit
             → 0 for power of 2

Prime      → check divisors up to √N

D digits   → O(D) = O(log N)

Digit loop:
while (num != 0)
```

---

# Final Interview Rule

When you see a **digit manipulation problem**, don't immediately think about complicated algorithms.

First think:

```text
Can I extract the digits using:

num % 10
num / 10
```

Then ask:

```text
What should I do with each digit?
```

That single question usually reveals the solution pattern.


---

# 27. Factorial

```cpp
long long result = 1;

for (int i = 2; i <= n; i++) {
    result *= i;
}
```

```text
Time  : O(N)
Space : O(1)
```

Remember:

```text
0! = 1
```

Factorial grows very quickly → watch for overflow.

---

# 28. GCD — Euclidean Algorithm

The most important identity:

```text
gcd(a, b) = gcd(b, a % b)
```

Template:

```cpp
while (b != 0) {
    int r = a % b;
    a = b;
    b = r;
}

return a;
```

Complexity:

```text
Time  : O(log(min(A, B)))
Space : O(1)
```

---

# 29. LCM

Formula:

```text
LCM(a, b) = (a / GCD(a, b)) × b
```

Prefer:

```cpp
(a / gcd) * b
```

rather than:

```cpp
(a * b) / gcd
```

because dividing first reduces overflow risk.

Complexity:

```text
Time  : O(log(min(A, B)))
Space : O(1)
```

---

# 30. Count Divisors

Divisors occur in pairs.

For `N = 36`:

```text
1 × 36
2 × 18
3 × 12
4 × 9
6 × 6
```

Therefore check only:

```cpp
for (int i = 1; i * i <= n; i++)
```

If `i` divides `n`:

```cpp
count++;
```

and count `n / i` too unless:

```cpp
i == n / i
```

Complexity:

```text
Time  : O(√N)
Space : O(1)
```

---

# 31. Narcissistic / Armstrong Number

A number with `D` digits is narcissistic if:

```text
sum of (each digit)^D = original number
```

Example:

```text
153

1³ + 5³ + 3³ = 153
```

Pattern:

```cpp
digits = countDigits(n);

while (n != 0) {
    digit = n % 10;
    sum += digit^digits;
    n /= 10;
}
```

Complexity:

```text
Time  : O(D)
Space : O(1)
```

---

# 32. 2's Complement

For a fixed-width binary number:

```text
1. Invert all bits
2. Add 1
```

Example:

```text
 5 = 00000101
~5 = 11111010
+1 = 11111011
```

C++ expression:

```cpp
~num + 1
```

### Important

2's complement depends on the chosen bit width.

---

# 33. Set the Kth Bit

Assume 0-based indexing.

```cpp
num | (1 << k)
```

Why?

```text
1 << k
```

creates a mask with only bit `k` set.

### Related operations

```cpp
// Set
num | (1 << k)

// Clear
num & ~(1 << k)

// Toggle
num ^ (1 << k)

// Check
(num >> k) & 1
```

Complexity:

```text
Time  : O(1)
Space : O(1)
```

---

# 34. Count Set Bits

### Basic

```cpp
while (n != 0) {
    count += (n & 1);
    n >>= 1;
}
```

### Brian Kernighan's Algorithm

```cpp
while (n != 0) {
    n = n & (n - 1);
    count++;
}
```

The operation:

```cpp
n & (n - 1)
```

removes the **lowest set bit**.

Complexity:

```text
Basic:
Time  : O(log N)
Space : O(1)

Kernighan:
Time  : O(K), K = number of set bits
Space : O(1)
```

---

# 35. Create a Number from Digits

Given:

```text
{1, 2, 3, 4}
```

construct:

```text
1234
```

Pattern:

```cpp
number = number * 10 + digit;
```

Example:

```text
0 → 1 → 12 → 123 → 1234
```

If there are `D` digits:

```text
Time  : O(D)
Space : O(1)
```

---

# 36. Print Digits

### `% 10` approach

Processes digits from right to left:

```cpp
while (num != 0) {
    int digit = num % 10;
    cout << digit;
    num /= 10;
}
```

Example:

```text
1234 → 4 3 2 1
```

### Left-to-right

Either:

- convert to a string, or
- find the highest power of `10` and extract digits from left to right.

---

# 37. Mathematical Conversions

## Kilometers → Miles

```text
miles = kilometers × 0.621371
```

## Celsius → Fahrenheit

```text
F = C × 9/5 + 32
```

## Fahrenheit → Celsius

```text
C = (F - 32) × 5/9
```

## Area of Circle

```text
Area = π × r²
```

These are all:

```text
Time  : O(1)
Space : O(1)
```

---

# 38. Print All Prime Numbers from 1 to N

Basic approach:

```cpp
for (int num = 2; num <= n; num++) {
    if (isPrime(num)) {
        cout << num << ' ';
    }
}
```

Using trial division up to `√num` for each number:

```text
Time ≈ O(N√N)
Space = O(1)
```

### Important optimization

If `N` is large and the task is specifically to find all primes up to `N`, think:

```text
Sieve of Eratosthenes
```

Do not automatically run a separate prime check for every number when constraints are large.

---

# 39. Extended Number-Problem Pattern Table

| Problem | Main Pattern | Typical Complexity |
|---|---|---|
| Sum of digits | `sum += digit` | `O(log N)` |
| Product of digits | `product *= digit` | `O(log N)` |
| Count digits | `count++` | `O(log N)` |
| Smallest digit | `min()` | `O(log N)` |
| Largest digit | `max()` | `O(log N)` |
| Reverse number | `ans*10 + digit` | `O(log N)` |
| Palindrome | Original == Reverse | `O(log N)` |
| Even/Odd | `% 2` / `& 1` | `O(1)` |
| Power of 2 | `n & (n-1)` | `O(1)` |
| Prime | Check to `√N` | `O(√N)` |
| Factorial | Repeated multiplication | `O(N)` |
| GCD | Euclidean algorithm | `O(log N)` |
| LCM | `a/gcd*b` | `O(log N)` |
| Count divisors | Divisor pairs | `O(√N)` |
| Narcissistic | Digit powers | `O(log N)` |
| 2's complement | `~n + 1` | `O(1)` |
| Set kth bit | `n \| (1 << k)` | `O(1)` |
| Count set bits | `n & (n-1)` | `O(K)` |
| Create number | `ans*10 + digit` | `O(D)` |
| Print digits | `%10`, `/10` | `O(D)` |
| KM → miles | Conversion formula | `O(1)` |
| Temperature | Conversion formula | `O(1)` |
| Circle area | `πr²` | `O(1)` |
| Primes 1..N | Prime check / sieve | `O(N√N)` / better with sieve |

---

# 40. Updated 30-Second Revision

```text
DIGITS
============================

% 10             → get last digit
/ 10             → remove last digit
ans*10 + digit   → build number / reverse

sum += digit     → sum
product *= digit → product
count++          → count
min(...)         → minimum
max(...)         → maximum
freq[digit]++    → frequency


NUMBER
============================

Palindrome:
    original == reverse

Prime:
    check i*i <= n

GCD:
    gcd(a,b) → gcd(b,a%b)

LCM:
    (a/gcd) * b

Factorial:
    result *= i

Divisors:
    check i*i <= n
    count paired divisors


BITS
============================

n & 1
    → odd/even

n & (n-1)
    → removes lowest set bit

n > 0 && (n & (n-1)) == 0
    → power of 2

n | (1 << k)
    → set kth bit

n & ~(1 << k)
    → clear kth bit

n ^ (1 << k)
    → toggle kth bit

(n >> k) & 1
    → check kth bit

~n + 1
    → 2's complement


MATH
============================

Area of circle:
    πr²

C → F:
    C*9/5 + 32

F → C:
    (F-32)*5/9

KM → miles:
    km*0.621371
```
