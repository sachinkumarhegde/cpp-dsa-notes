# Time & Space Complexity

> **Purpose:** Revision notes  
> **Goal:** Quickly recall the concepts, rules, and common patterns without going into textbook-level detail.

---

## 1. Time Complexity

### Definition

**Time complexity** describes how the running time of an algorithm grows with respect to the input size `n`.

It does **not** represent the actual execution time in seconds.

### Why not measure actual time?

Actual execution time depends on:

- Processor
- RAM
- Programming language
- Compiler
- Operating system
- System load

Therefore, we analyze how the **number of operations grows as `n` increases**.

### Example

for (int i = 0; i < n; i++) {
    cout << i;
}

The loop executes `n` times.

**Time Complexity: `O(n)`**

---

# 2. Space Complexity

### Definition

**Space complexity** describes how the memory requirement of an algorithm grows with respect to input size `n`.

### Example — O(1)

int sum = 0;

for (int i = 0; i < n; i++) {
    sum += i;
}

Only a fixed number of variables are used.

**Auxiliary Space: `O(1)`**

### Example — O(n)

int arr[n];

Memory grows with `n`.

**Space Complexity: `O(n)`**

### Important Interview Point

Distinguish between:

- **Input space** → memory required to store the input
- **Auxiliary space** → extra memory used by the algorithm

In interviews, when someone asks for the space complexity of an algorithm, they often mean **auxiliary space**.

---

# 3. Why Complexity Analysis?

Complexity analysis helps us:

1. Compare different algorithms.
2. Predict how an algorithm behaves for large inputs.
3. Identify inefficient solutions.
4. Optimize CPU and memory usage.
5. Explain the efficiency of a solution during interviews.

### Example

For searching an element:

- Linear Search → `O(n)`
- Binary Search → `O(log n)`

For a large sorted array, Binary Search scales much better.

---

# 4. Asymptotic Notation

The three important notations are:

| Notation | Meaning |
|---|---|
| `O(f(n))` | Upper bound |
| `Ω(f(n))` | Lower bound |
| `Θ(f(n))` | Tight bound |

## 4.1 Big O — O

Big O represents an **upper bound** on the growth of an algorithm.

Interview intuition:

> "The algorithm grows no faster than this order."

Example:

`O(n)`

## 4.2 Omega — Ω

Omega represents a **lower bound**.

Interview intuition:

> "The algorithm requires at least this order of growth."

Example:

`Ω(n)`

## 4.3 Theta — Θ

Theta represents a **tight asymptotic bound**.

Interview intuition:

> "The algorithm grows at this asymptotic order."

Example:

`Θ(n)`

### Important

`Θ` does **not** mean average case.

Average-case complexity is a separate concept.

---

# 5. Common Time Complexities

From generally better scaling to worse scaling:

O(1)
O(log n)
O(√n)
O(n)
O(n log n)
O(n²)
O(n³)
O(2ⁿ)

### Growth order to memorize

`O(1) < O(log n) < O(√n) < O(n) < O(n log n) < O(n²) < O(n³) < O(2ⁿ)`

As `n` becomes very large, the difference between these complexities becomes significant.

---

# 6. O(1) — Constant Time

The amount of work does not depend on `n`.

### Example

int x = arr[5];

Accessing a known array index takes constant time.

**Time Complexity: `O(1)`**

### Common examples

- Array access by index
- Stack push/pop
- Stack top
- Basic arithmetic
- Variable assignment

---

# 7. O(log n) — Logarithmic Time

The input size is repeatedly reduced by a constant factor.

Most commonly:

n → n/2 → n/4 → n/8 → ... → 1

The number of operations is approximately `log₂(n)`.

### Example

while (n > 1) {
    n = n / 2;
}

**Time Complexity: `O(log n)`**

### Classic Example

**Binary Search**

At every step, approximately half of the search space is eliminated.

**Binary Search: `O(log n)`**

### Interview clue

If you see repeated division/multiplication by a constant, think:

**`O(log n)`**

---

# 8. O(√n) — Square Root Time

An algorithm performs work up to `√n`.

### Example

Checking whether a number is prime:

for (int i = 2; i * i <= n; i++) {
    // check divisibility
}

The loop runs approximately `√n` times.

**Time Complexity: `O(√n)`**

### Example

For `n = 1,000,000`:

`√n = 1,000`

So checking only up to `√n` is much better than checking all `n` values.

---

# 9. O(n) — Linear Time

Work grows directly with the input size.

### Example

for (int i = 0; i < n; i++) {
    cout << i;
}

The loop runs `n` times.

**Time Complexity: `O(n)`**

### Classic Example

**Linear Search**

In the worst case, every element may be examined.

**Time Complexity: `O(n)`**

---

# 10. O(n log n)

Very common in efficient sorting algorithms.

### Examples

- Merge Sort
- Heap Sort
- Average-case Quick Sort

A common pattern is:

`n work × log n levels`

Therefore:

**`O(n log n)`**

`O(n log n)` is significantly better than `O(n²)` for large inputs.

---

# 11. O(n²) — Quadratic Time

Usually occurs with two nested loops.

### Example

for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        // operation
    }
}

Total operations:

`n × n = n²`

**Time Complexity: `O(n²)`**

### Common examples

- Bubble Sort
- Selection Sort
- Comparing every pair of elements

### Interview clue

Two nested loops, each running `n` times:

**`O(n²)`**

---

# 12. O(n³) — Cubic Time

Usually occurs with three nested loops.

### Example

for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        for (int k = 0; k < n; k++) {
            // operation
        }
    }
}

Total:

`n × n × n = n³`

**Time Complexity: `O(n³)`**

Often seen in brute-force algorithms involving three elements or some matrix operations.

---

# 13. O(2ⁿ) — Exponential Time

The amount of work grows exponentially with `n`.

A classic example is naive recursive Fibonacci:

int fib(int n) {
    if (n <= 1)
        return n;

    return fib(n - 1) + fib(n - 2);
}

The recursion creates many repeated calls.

**Time Complexity: approximately `O(2ⁿ)`**

### Why is it dangerous?

2¹⁰ ≈ 1 thousand
2²⁰ ≈ 1 million
2³⁰ ≈ 1 billion

Exponential algorithms become impractical very quickly.

---

# 14. Constant Factors

Consider:

for (int i = 0; i < n; i++) {
    // operation
}

for (int i = 0; i < n; i++) {
    // operation
}

Total:

`n + n = 2n`

Therefore:

`O(2n) = O(n)`

### Examples

O(5n)      → O(n)
O(100n)    → O(n)
O(3n²)     → O(n²)
O(50n³)    → O(n³)

### Rule

**Ignore constant multipliers in asymptotic complexity.**

---

# 15. Dominant Term

Consider:

`O(n² + n + 10)`

For large `n`, `n²` dominates.

Therefore:

`O(n² + n + 10) → O(n²)`

### Examples

O(n² + n)          → O(n²)
O(n³ + n² + n)     → O(n³)
O(n + log n)       → O(n)
O(n log n + n)     → O(n log n)
O(2ⁿ + n²)         → O(2ⁿ)

### Rule

**Keep the fastest-growing term.**

---

# 16. Sequential vs Nested Loops

## Sequential Operations

Complexities are added.

for (...) {
    // O(n)
}

for (...) {
    // O(n)
}

Total:

`O(n + n) = O(2n) = O(n)`

## Nested Operations

Complexities are multiplied.

for (...) {          // O(n)
    for (...) {      // O(n)
    }
}

Total:

`O(n × n) = O(n²)`

### Interview Rule

> **Sequential → Add**

> **Nested → Multiply**

---

# 17. Different-Sized Nested Loops

Do not blindly assume every nested loop is `O(n²)`.

for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
        // operation
    }
}

Complexity:

**`O(n × m)`**

Only when `m ≈ n` can we simplify it to:

**`O(n²)`**

### Interview Point

Always identify the actual loop bounds.

---

# 18. Loops with Different Growth Rates

Example:

for (int i = 0; i < n; i++) {
    // O(n)
}

for (int i = 1; i < n; i *= 2) {
    // O(log n)
}

Total:

`O(n + log n)`

Dominant term is `n`.

Therefore:

**`O(n)`**

---

# 19. Linear Search vs Binary Search

## Linear Search

Works on an unsorted array.

Worst case:

**`O(n)`**

## Binary Search

Requires a **sorted** search space.

At every step, approximately half of the search space is eliminated.

**`O(log n)`**

### Comparison

| Algorithm | Requirement | Time |
|---|---|---:|
| Linear Search | No sorting required | `O(n)` |
| Binary Search | Sorted data | `O(log n)` |

### Interview Point

> Binary Search is efficient because it eliminates approximately half of the search space at every step.

---

# 20. Recursion and Complexity

When analyzing recursive algorithms, consider:

1. Number of recursive calls
2. Work performed in each call
3. Number of recursion levels

### Example — One Recursive Call

void func(int n) {
    if (n <= 1)
        return;

    func(n / 2);
}

Each call reduces `n` by half.

Number of levels:

`log n`

**Time: `O(log n)`**

### Example — Two Recursive Calls

func(n - 1);
func(n - 2);

This creates a branching recursion tree.

Naive Fibonacci:

**Time: approximately `O(2ⁿ)`**

---

# 21. Recursion Space Complexity

Recursive calls consume **call stack memory**.

Example:

void func(int n) {
    if (n == 0)
        return;

    func(n - 1);
}

There are `n` active function calls.

**Auxiliary Space: `O(n)`**

### Important

> **Maximum recursion depth often determines stack space.**

---

# 22. Time-Space Trade-off

Sometimes we use more memory to make an algorithm faster.

### Without storing results

Repeated computation
→ More time
→ Less memory

### With memoization

Store previously calculated results
→ Less repeated work
→ More memory

This is called a:

**Time-Space Trade-off**

### Common examples

- Hash tables
- Memoization
- Dynamic Programming
- Caching

---

# 23. Best, Average and Worst Case

An algorithm can behave differently depending on the input.

### Best Case

Minimum amount of work.

### Average Case

Expected work over typical/random inputs.

### Worst Case

Maximum amount of work.

### Example — Linear Search

Searching for the first element:

**Best Case: `O(1)`**

Searching for the last element or an absent element:

**Worst Case: `O(n)`**

### Important

Do not confuse:

Best / Average / Worst Case

with:

O / Ω / Θ

They describe different concepts.

---

# 24. Complexity of Common Operations

## Array

| Operation | Complexity |
|---|---:|
| Access by index | `O(1)` |
| Search | `O(n)` |
| Insert at end* | `O(1)` |
| Insert at beginning | `O(n)` |
| Delete at end* | `O(1)` |
| Delete at beginning | `O(n)` |

`*` Assumes enough capacity / appropriate array structure.

## Stack

| Operation | Complexity |
|---|---:|
| Push | `O(1)` |
| Pop | `O(1)` |
| Top | `O(1)` |
| Search | `O(n)` |

## Queue

| Operation | Complexity |
|---|---:|
| Enqueue | `O(1)` |
| Dequeue | `O(1)` |
| Front | `O(1)` |
| Search | `O(n)` |

---

# 25. Complexity Recognition Patterns

| Code Pattern | Typical Complexity |
|---|---:|
| Single statement | `O(1)` |
| Single loop `0 → n` | `O(n)` |
| Loop repeatedly dividing by 2 | `O(log n)` |
| Loop up to `√n` | `O(√n)` |
| Two independent `n` loops | `O(n)` |
| Two nested `n` loops | `O(n²)` |
| Three nested `n` loops | `O(n³)` |
| Divide and process all `n` elements | Often `O(n log n)` |
| Naive branching recursion | Often exponential |

---

# 26. How to Calculate Complexity in an Interview

### Step 1 — Identify the input size

Usually:

`n`

But it could be:

`n, m`

or multiple dimensions.

### Step 2 — Count loop iterations

Ask:

> How many times does this loop execute?

Typical patterns:

```text
i++          → O(n)
i *= 2       → O(log n)
i /= 2       → O(log n)
i*i <= n     → O(√n)
```

### Step 3 — Check nesting

**Nested loops → Multiply**

Example:

`O(n) × O(n) = O(n²)`

### Step 4 — Check sequential blocks

**Sequential blocks → Add**

Example:

`O(n) + O(n²) = O(n²)`

### Step 5 — Remove constants

`O(5n) → O(n)`

### Step 6 — Remove lower-order terms

`O(n² + n + 1) → O(n²)`

### Step 7 — Analyze space

Check for:

- Arrays
- Vectors
- Hash maps
- Extra data structures
- Recursion stack
- Dynamic allocations

---

# 27. Important Interview Traps

## Trap 1 — Nested loops do not always mean O(n²)

for (int i = 0; i < n; i++) {
    for (int j = 0; j < 100; j++) {
        // operation
    }
}

Complexity:

`O(n × 100) = O(n)`

Because `100` is constant.

---

## Trap 2 — Two loops do not always mean O(n²)

for (int i = 0; i < n; i++) { }

for (int i = 0; i < n; i++) { }

Complexity:

`O(n + n) = O(n)`

---

## Trap 3 — Loop variable does not always increase by 1

for (int i = 1; i < n; i *= 2) {
}

Complexity:

**`O(log n)`**

---

## Trap 4 — Input dimensions may be different

for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
    }
}

Complexity:

**`O(nm)`**

Not automatically `O(n²)`.

---

## Trap 5 — Recursion uses stack space

Even if no explicit array/vector is created, recursive calls consume stack memory.

---

# 28. Quick Interview Cheat Sheet

## Complexity Order

O(1)
    ↓
O(log n)
    ↓
O(√n)
    ↓
O(n)
    ↓
O(n log n)
    ↓
O(n²)
    ↓
O(n³)
    ↓
O(2ⁿ)

## Asymptotic Notation

O      → Upper Bound
Ω      → Lower Bound
Θ      → Tight Bound

## Core Rules

Sequential operations → Add

Nested operations → Multiply

Ignore constants
→ O(2n) = O(n)

Ignore lower-order terms
→ O(n² + n) = O(n²)

Repeatedly divide by 2
→ O(log n)

Loop up to √n
→ O(√n)

Two n-sized nested loops
→ O(n²)

Three n-sized nested loops
→ O(n³)

## Most Important Examples

Array access             → O(1)

Linear Search            → O(n)

Binary Search            → O(log n)

Prime checking           → O(√n)

Merge Sort               → O(n log n)

Bubble Sort              → O(n²)

Selection Sort           → O(n²)

Naive Fibonacci          → O(2ⁿ)

---

# 29. Final Interview Recall

Before an interview, make sure you can answer these without looking at notes:

1. What is time complexity?
2. What is space complexity?
3. What is auxiliary space?
4. What are `O`, `Ω`, and `Θ`?
5. Difference between Big O and Theta?
6. Why do we ignore constants?
7. Why do we ignore lower-order terms?
8. Why is Binary Search `O(log n)`?
9. Why is Linear Search `O(n)`?
10. Why are two nested loops usually `O(n²)`?
11. Why are sequential loops added instead of multiplied?
12. How do you identify `O(log n)` from code?
13. How do you identify `O(√n)`?
14. How does recursion affect space complexity?
15. What is the difference between best, average, and worst case?
16. What is the difference between `O(n)` and `O(n log n)`?
17. Why does exponential complexity become impractical?
18. What is a time-space trade-off?

---

# 30. One-Minute Revision

> **Time complexity** → How runtime grows with input size.

> **Space complexity** → How memory usage grows with input size.

> **O(1)** → Constant

> **O(log n)** → Repeatedly divide the problem

> **O(√n)** → Work up to square root of input

> **O(n)** → Process input once

> **O(n log n)** → Efficient divide-and-conquer/sorting pattern

> **O(n²)** → Compare pairs / two nested loops

> **O(n³)** → Three nested loops

> **O(2ⁿ)** → Exponential branching

> **Sequential** → Add

> **Nested** → Multiply

> **Ignore constants and lower-order terms**

> **Always analyze both time and auxiliary space.**
