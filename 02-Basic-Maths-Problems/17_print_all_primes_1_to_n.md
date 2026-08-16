# Print All Prime Numbers from 1 to N

## Problem

Print every prime number between `1` and `N`.

Example:

```text
N = 10

2 3 5 7
```

## Approach

For each number, check whether it is prime.

Use the optimized prime check up to `sqrt(number)`.

## C++ Program

```cpp
#include <iostream>

bool isPrime(int num) {

    // Numbers <= 1 are not prime.
    if (num <= 1) {
        return false;
    }

    // Only check divisors up to sqrt(num).
    for (int i = 2; i * i <= num; i++) {

        if (num % i == 0) {
            return false;
        }
    }

    return true;
}

void printPrimes(int n) {

    for (int num = 2; num <= n; num++) {

        // Print num if it is prime.
        if (isPrime(num)) {
            std::cout << num << ' ';
        }
    }
}
```

## Complexity

Using trial division for every number:

- Time: approximately `O(N√N)`
- Space: `O(1)`

## Interview Note

If `N` is very large and the problem asks for many primes up to `N`, consider the **Sieve of Eratosthenes**, which is much more efficient.
