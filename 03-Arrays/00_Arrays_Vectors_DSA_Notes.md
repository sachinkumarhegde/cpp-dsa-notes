# Arrays & Vectors — C++17 DSA Interview Notes

> **Goal:** Quick revision of the concepts needed to solve array/vector problems from easy to difficult.

---

## 1. Array Basics

### Declaration

```cpp
int arr[5];
int arr[5] = {1, 2, 3, 4, 5};
int arr[] = {1, 2, 3};
```

- Fixed size.
- Elements stored in **contiguous memory**.
- Index starts from `0`.
- Access: `arr[i]` → **O(1)**.

### Important Operations

| Operation | Complexity |
|---|---:|
| Access by index | O(1) |
| Update by index | O(1) |
| Search (unsorted) | O(n) |
| Search (sorted, binary search) | O(log n) |
| Insert/delete at end* | O(1) |
| Insert/delete in middle | O(n) |

\*For a fixed array, size cannot actually change; this applies when using an appropriate dynamic structure.

### Array Size

```cpp
int arr[5];
int n = sizeof(arr) / sizeof(arr[0]);
```

`sizeof(arr)` gives total bytes; divide by one element's size.

---

## 2. Traversing an Array

### Index-based

```cpp
for (int i = 0; i < n; i++)
    cout << arr[i];
```

### Range-based

```cpp
for (int x : arr)
    cout << x;
```

### Modify elements

```cpp
for (int& x : arr)
    x *= 2;
```

Use `&` when you want to modify the original elements.

---

## 3. Passing Arrays to Functions

```cpp
void print(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i];
}
```

An array passed to a function generally **decays to a pointer**, so the size is usually passed separately.

For fixed-size arrays, `std::array` can preserve size information.

---

# 4. Vector

`vector` is the most commonly used dynamic array in C++ DSA.

```cpp
#include <vector>
using namespace std;

vector<int> v;
vector<int> v = {1, 2, 3};
vector<int> v(5);       // 5 elements, initialized to 0
vector<int> v(5, 10);   // 5 elements, all 10
```

### Common Functions

```cpp
v.push_back(10);     // add at end
v.pop_back();        // remove last
v.size();            // number of elements
v.empty();           // true/false
v.front();
v.back();
v.clear();
v[2];
v.at(2);
```

### Insert / Erase

```cpp
v.insert(v.begin() + 2, 100);
v.erase(v.begin() + 2);
```

Insertion/deletion in the middle is **O(n)** because elements may need to shift.

---

## 5. Vector Capacity vs Size

```cpp
v.size();      // number of actual elements
v.capacity();  // allocated storage
```

When capacity is insufficient, vector allocates a larger memory block and moves/copies elements.

```cpp
v.reserve(100);
```

`reserve()` changes capacity, **not size**.

```cpp
v.resize(100);
```

`resize()` changes the number of elements.

---

## 6. Vector Complexity

| Operation | Average |
|---|---:|
| Access | O(1) |
| `push_back()` | O(1) amortized |
| `pop_back()` | O(1) |
| Insert middle | O(n) |
| Erase middle | O(n) |
| Search | O(n) |
| Sort | O(n log n) |

### Amortized O(1)

`push_back()` is usually O(1), but occasionally a resize/reallocation costs O(n).

Over many insertions, the **average cost per insertion is O(1)**.

---

# 7. 2D Arrays

### Declaration

```cpp
int matrix[3][4];
```

3 rows × 4 columns.

### Initialization

```cpp
int matrix[2][3] = {
    {1, 2, 3},
    {4, 5, 6}
};
```

### Access

```cpp
matrix[1][2];
```

### Traversal

```cpp
for (int i = 0; i < rows; i++)
{
    for (int j = 0; j < cols; j++)
        cout << matrix[i][j];
}
```

---

# 8. Vector of Vectors

Used for dynamic 2D arrays/matrices.

```cpp
vector<vector<int>> matrix(
    rows, vector<int>(cols)
);
```

Example:

```cpp
vector<vector<int>> matrix = {
    {1, 2, 3},
    {4, 5, 6}
};
```

Access:

```cpp
matrix[i][j];
```

Traversal:

```cpp
for (const auto& row : matrix)
{
    for (int x : row)
        cout << x;
}
```

Rows can have different sizes:

```cpp
vector<vector<int>> v = {
    {1, 2},
    {3, 4, 5},
    {6}
};
```

---

# 9. Array / Vector Searching

### Linear Search

```cpp
for (int i = 0; i < n; i++)
{
    if (arr[i] == target)
        return i;
}
```

**Time:** O(n)

---

## 10. Binary Search

Applicable when the data is **sorted**.

```cpp
int low = 0, high = n - 1;

while (low <= high)
{
    int mid = low + (high - low) / 2;

    if (arr[mid] == target)
        return mid;
    else if (arr[mid] < target)
        low = mid + 1;
    else
        high = mid - 1;
}
```

**Time:** O(log n)

Important pattern:

> Sorted array + search for a value/position → think **binary search**.

---

# 11. STL Binary Search Functions

```cpp
binary_search(v.begin(), v.end(), x);
```

Returns `true/false`.

```cpp
lower_bound(v.begin(), v.end(), x);
```

Returns iterator to the **first position where value >= x**.

```cpp
upper_bound(v.begin(), v.end(), x);
```

Returns iterator to the **first position where value > x**.

Index:

```cpp
int index = lower_bound(v.begin(), v.end(), x) - v.begin();
```

### Key Difference

For sorted:

`[1, 2, 2, 2, 4]`

- `lower_bound(2)` → first `2`
- `upper_bound(2)` → position after last `2`

---

# 12. Sorting

```cpp
sort(v.begin(), v.end());
sort(v.begin(), v.end(), greater<int>());
```

**Time:** O(n log n)

Sorting is often useful for simplifying array problems involving:

- duplicates
- pairs
- intervals
- two pointers
- greedy approaches

---

# 13. Reverse

```cpp
reverse(v.begin(), v.end());
```

**Time:** O(n)

---

# 14. Min / Max

```cpp
#include <algorithm>

int mn = *min_element(v.begin(), v.end());
int mx = *max_element(v.begin(), v.end());
```

---

# 15. Frequency Counting

When values have a limited range:

```cpp
vector<int> freq(101, 0);

for (int x : v)
    freq[x]++;
```

Useful for:

- duplicate detection
- counting occurrences
- finding most/least frequent values
- anagram-style problems

If values are large/arbitrary, use:

```cpp
unordered_map<int, int> freq;
```

---

# 16. Prefix Sum

Used when many **range-sum queries** are required.

Array:

```text
[2, 4, 1, 5, 3]
```

Prefix:

```text
[0, 2, 6, 7, 12, 15]
```

Build:

```cpp
vector<int> prefix(n + 1, 0);

for (int i = 0; i < n; i++)
    prefix[i + 1] = prefix[i] + arr[i];
```

Sum from `l` to `r`:

```cpp
sum = prefix[r + 1] - prefix[l];
```

### Complexity

- Build: O(n)
- Each range query: O(1)

---

# 17. Difference Array

Useful when performing many **range updates**.

To add `x` to `[l, r]`:

```cpp
diff[l] += x;
diff[r + 1] -= x;
```

Then calculate prefix sums of `diff` to obtain the final array.

Pattern:

> Many range updates → **Difference Array**

---

# 18. Two Pointers

Common for sorted arrays or problems involving pairs/subarrays.

Example: pair with target sum.

```cpp
int l = 0, r = n - 1;

while (l < r)
{
    int sum = arr[l] + arr[r];

    if (sum == target)
        return true;
    else if (sum < target)
        l++;
    else
        r--;
}
```

**Time:** O(n) after sorting.

Typical clues:

- pair/triplet
- sorted array
- target sum
- remove duplicates
- opposite ends

---

# 19. Sliding Window

Used for **contiguous subarrays/substrings**.

Example: maximum sum of subarray of size `k`.

```cpp
int sum = 0;

for (int i = 0; i < k; i++)
    sum += arr[i];

int ans = sum;

for (int i = k; i < n; i++)
{
    sum += arr[i];
    sum -= arr[i - k];
    ans = max(ans, sum);
}
```

**Time:** O(n)

### Fixed Window

Window size is fixed.

### Variable Window

Window expands/shrinks based on a condition.

Common clues:

> "longest/shortest subarray satisfying..."  
> "at most K..."  
> "sum <= target..."

---

# 20. Kadane's Algorithm

Find maximum subarray sum.

```cpp
int current = arr[0];
int best = arr[0];

for (int i = 1; i < n; i++)
{
    current = max(arr[i], current + arr[i]);
    best = max(best, current);
}
```

**Time:** O(n)  
**Space:** O(1)

Core idea:

> At every element, decide whether to **extend** the previous subarray or **start new**.

---

# 21. Subarray vs Subsequence vs Subset

### Subarray

Contiguous.

```text
[2, 3, 4]
```

from:

```text
[1, 2, 3, 4, 5]
```

### Subsequence

Order preserved, but elements need not be contiguous.

```text
[1, 3, 5]
```

### Subset

Order generally does not matter.

Important distinction because the solution technique changes significantly.

---

# 22. In-place Array Manipulation

Many interview problems require:

> "Do it without extra array."

Use techniques such as:

- swapping
- two pointers
- overwriting
- partitioning

Example: move zeroes.

```cpp
int j = 0;

for (int i = 0; i < n; i++)
{
    if (arr[i] != 0)
        swap(arr[i], arr[j++]);
}
```

**Time:** O(n)  
**Extra space:** O(1)

---

# 23. Partitioning

Partition elements based on a condition.

Example:

```text
Even / Odd
Positive / Negative
0 / Non-zero
```

Two-pointer pattern:

```cpp
int i = 0, j = n - 1;

while (i < j)
{
    while (i < j && condition(arr[i]))
        i++;

    while (i < j && !condition(arr[j]))
        j--;

    if (i < j)
        swap(arr[i], arr[j]);
}
```

---

# 24. Dutch National Flag

Classic problem: sort `0, 1, 2`.

Maintain:

```text
[0 ... low-1]     → 0
[low ... mid-1]   → 1
[mid ... high]    → unknown
[high+1 ... n-1]  → 2
```

```cpp
int low = 0, mid = 0, high = n - 1;

while (mid <= high)
{
    if (arr[mid] == 0)
        swap(arr[low++], arr[mid++]);
    else if (arr[mid] == 1)
        mid++;
    else
        swap(arr[mid], arr[high--]);
}
```

**Time:** O(n)  
**Space:** O(1)

---

# 25. Rotation

### Left rotate by one

```cpp
int first = arr[0];

for (int i = 1; i < n; i++)
    arr[i - 1] = arr[i];

arr[n - 1] = first;
```

### Rotate using reverse

For left rotation by `k`:

```text
reverse(0, k-1)
reverse(k, n-1)
reverse(0, n-1)
```

Always do:

```cpp
k %= n;
```

before rotation.

---

# 26. Missing Number

For values `0 ... n`, use XOR or sum.

### XOR approach

```cpp
int ans = n;

for (int i = 0; i < n; i++)
    ans ^= i ^ arr[i];
```

Why XOR?

```text
x ^ x = 0
x ^ 0 = x
```

Duplicates cancel.

**Time:** O(n)  
**Space:** O(1)

---

# 27. Duplicate Detection

Simple approaches:

### Sorting

```cpp
sort(v.begin(), v.end());

for (int i = 1; i < n; i++)
    if (v[i] == v[i - 1])
        return true;
```

**Time:** O(n log n)

### Hash Set

```cpp
unordered_set<int> seen;

for (int x : v)
{
    if (seen.count(x))
        return true;

    seen.insert(x);
}
```

Average **O(n)** time, O(n) space.

Choose based on whether extra space is allowed.

---

# 28. Hashing + Array Problems

Useful when looking for:

- Two Sum
- duplicates
- frequencies
- longest subarray
- counts of previous values

Example Two Sum:

```cpp
unordered_map<int, int> mp;

for (int i = 0; i < n; i++)
{
    int need = target - arr[i];

    if (mp.count(need))
        return {mp[need], i};

    mp[arr[i]] = i;
}
```

Average:

**Time:** O(n)  
**Space:** O(n)

---

# 29. Prefix Sum + Hash Map

Important advanced pattern.

Used for problems such as:

- subarray sum equals K
- longest subarray with a particular sum
- count of subarrays satisfying a sum condition

Core idea:

```text
prefixSum[i] - prefixSum[j] = target
```

Therefore:

```text
prefixSum[j] = prefixSum[i] - target
```

Store previously seen prefix sums in a hash map.

---

# 30. Maximum / Minimum Subarray Patterns

Recognize these separately:

### Maximum sum

→ Kadane

### Fixed-size maximum sum

→ Sliding window

### Longest subarray satisfying condition

→ Variable sliding window / prefix sum + map

### Count subarrays with target sum

→ Prefix sum + hash map

---

# 31. 2D Matrix Traversal Patterns

## Row-wise

```cpp
for (int i = 0; i < rows; i++)
    for (int j = 0; j < cols; j++)
        process(matrix[i][j]);
```

## Column-wise

```cpp
for (int j = 0; j < cols; j++)
    for (int i = 0; i < rows; i++)
        process(matrix[i][j]);
```

## Main diagonal

For a square matrix:

```cpp
for (int i = 0; i < n; i++)
    process(matrix[i][i]);
```

## Anti-diagonal

```cpp
for (int i = 0; i < n; i++)
    process(matrix[i][n - 1 - i]);
```

---

# 32. Matrix Transpose

For square matrix:

```cpp
for (int i = 0; i < n; i++)
{
    for (int j = i + 1; j < n; j++)
        swap(matrix[i][j], matrix[j][i]);
}
```

Important:

> Start `j` from `i + 1` to avoid swapping elements twice.

---

# 33. Rotate Matrix 90° Clockwise

For a square matrix:

1. Transpose
2. Reverse every row

```cpp
// transpose
for (int i = 0; i < n; i++)
    for (int j = i + 1; j < n; j++)
        swap(matrix[i][j], matrix[j][i]);

// reverse each row
for (auto& row : matrix)
    reverse(row.begin(), row.end());
```

**Time:** O(n²)  
**Extra space:** O(1), excluding the matrix itself.

---

# 34. Spiral Matrix

Typical approach:

Maintain four boundaries:

```text
top
bottom
left
right
```

Traverse:

```text
left → right
top → bottom
right → left
bottom → top
```

After each traversal, move the corresponding boundary inward.

Be careful with single-row/single-column remaining regions.

---

# 35. Search in Sorted Matrix

For a matrix sorted:

- each row sorted
- each column sorted

Start from the **top-right**.

```cpp
int i = 0;
int j = cols - 1;

while (i < rows && j >= 0)
{
    if (matrix[i][j] == target)
        return true;
    else if (matrix[i][j] > target)
        j--;
    else
        i++;
}
```

**Time:** O(rows + cols)

---

# 36. Common Array Problem Patterns

| Problem clue | Think |
|---|---|
| Direct index access | Array / vector |
| Sorted + search | Binary search |
| Pair in sorted array | Two pointers |
| Contiguous + fixed K | Sliding window |
| Longest/shortest subarray | Sliding window / prefix sum |
| Maximum subarray sum | Kadane |
| Many range sums | Prefix sum |
| Many range updates | Difference array |
| Frequency | Hash map / frequency array |
| Duplicate | Set / sort |
| Target pair | Hash map / two pointers |
| In-place | Two pointers / swapping |
| 0,1,2 partition | Dutch National Flag |
| Rotate array | Reverse technique |
| Matrix boundary traversal | Boundary / spiral |
| Matrix 90° rotation | Transpose + reverse |
| Sorted matrix | Staircase search |

---

# 37. Brute Force → Optimized Thinking

For every array problem, ask:

### 1. Can I solve it by brute force?

Usually:

```text
O(n²) / O(n³)
```

### 2. What repeated work exists?

Look for:

- repeated sums
- repeated searches
- repeated counting
- repeated subarray calculations

### 3. Can I use:

- Hashing?
- Sorting?
- Two pointers?
- Sliding window?
- Prefix sum?
- Binary search?
- Greedy?
- In-place modification?

### 4. Can space be reduced?

Example:

```text
O(n) → O(1)
```

if only a few variables are needed.

---

# 38. Important C++ Vector Pitfalls

### Don't access empty vector

```cpp
v[0];       // undefined behavior if empty
```

Check:

```cpp
if (!v.empty())
```

### Iterator invalidation

Operations such as vector reallocation can invalidate iterators/references/pointers to elements.

### `size()` returns unsigned type

```cpp
for (int i = 0; i < v.size(); i++)
```

Usually works for normal cases, but mixing signed and unsigned types can cause warnings/issues.

### Don't use `reserve()` when you mean `resize()`

```cpp
v.reserve(10); // capacity only
v.resize(10);  // creates 10 elements
```

---

# 39. Useful STL Algorithms

```cpp
sort(v.begin(), v.end());

reverse(v.begin(), v.end());

find(v.begin(), v.end(), x);

count(v.begin(), v.end(), x);

min_element(v.begin(), v.end());

max_element(v.begin(), v.end());

binary_search(v.begin(), v.end(), x);

lower_bound(v.begin(), v.end(), x);

upper_bound(v.begin(), v.end(), x);
```

Header:

```cpp
#include <algorithm>
```

---

# 40. Complexity Checklist

Before finalizing an array solution, state:

```text
Time Complexity: O(...)
Space Complexity: O(...)
```

Remember:

- One pass → O(n)
- Nested full loops → O(n²)
- Sorting → O(n log n)
- Binary search → O(log n)
- Hashing → average O(1) per operation
- Extra array/map/set → usually O(n) space

---

# 41. Array DSA Progression

Recommended order for practice:

### Level 1 — Basics

- Traversal
- Sum / average
- Min / max
- Reverse
- Linear search
- Frequency
- Duplicate detection

### Level 2 — Easy Interview Problems

- Second largest
- Move zeroes
- Remove duplicates
- Rotate array
- Missing number
- Intersection / union
- Two Sum
- Merge sorted arrays

### Level 3 — Core Patterns

- Two pointers
- Sliding window
- Prefix sum
- Hashing
- Kadane
- Binary search
- Partitioning

### Level 4 — Medium

- 3Sum
- Majority element
- Sort 0/1/2
- Subarray sum = K
- Longest subarray
- Product except self
- Merge intervals
- Next permutation
- Stock buy/sell
- Search rotated sorted array

### Level 5 — Advanced

- Binary search on answer
- Monotonic stack + arrays
- Prefix sum + hashing
- Difference arrays
- Kadane variations
- Maximum product subarray
- Trapping rain water
- Sliding window with frequency maps
- Matrix spiral/rotation/search
- 2D prefix sums

---

# 42. Quick Recognition Rules

When you see an array problem, ask:

```text
Is it sorted?
    → Binary Search / Two Pointers

Is it about a pair?
    → Hashing / Two Pointers

Is it contiguous?
    → Sliding Window / Prefix Sum / Kadane

Are there repeated range sums?
    → Prefix Sum

Are there repeated range updates?
    → Difference Array

Are frequencies important?
    → Hash Map / Frequency Array

Is extra space prohibited?
    → In-place / Two Pointers / Swapping

Is it a matrix?
    → Boundary / Diagonal / Spiral / Transpose

Can sorting simplify the problem?
    → Sort + Two Pointers / Greedy

Do I need the best possible O(n)?
    → Look for a known array pattern
```

---

# 43. Final Interview Checklist

Before coding:

- [ ] Understand whether array is sorted.
- [ ] Check constraints.
- [ ] Identify contiguous vs non-contiguous.
- [ ] Try brute force mentally.
- [ ] Identify repeated work.
- [ ] Choose the appropriate pattern.
- [ ] Check edge cases.
- [ ] Consider integer overflow.
- [ ] Decide whether extra space is allowed.
- [ ] State time and space complexity.

### Common Edge Cases

```text
n = 0
n = 1
all elements equal
already sorted
reverse sorted
all negative
all positive
duplicates
target absent
target at first/last position
k > n
k = 0
```

---

## Core Patterns to Master

If you master these, you can solve a large portion of array interview problems:

1. **Traversal**
2. **Sorting**
3. **Hashing**
4. **Two Pointers**
5. **Sliding Window**
6. **Prefix Sum**
7. **Difference Array**
8. **Binary Search**
9. **Kadane's Algorithm**
10. **In-place / Partitioning**
11. **Matrix Traversal**
12. **Matrix Transformation**
13. **Monotonic Stack**
14. **Binary Search on Answer**

> **Key mindset:** Don't memorize individual solutions. Learn to recognize the pattern behind the problem.
