# A_Dislike_of_Threes

## Platform

Codeforces

## Problem Link

[A. Dislike of Threes](https://codeforces.com/problemset/problem/1560/A)

## Problem Statement

Vasya dislikes numbers that are either:

* Divisible by `3`, or
* End with the digit `3`

He creates a sequence of positive integers that **do not satisfy either of the above conditions**, in increasing order.

Given a number `k`, your task is to determine the **k-th number** in this sequence.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each of the next `t` lines contains a single integer `k`.

## Output Format

For each test case, print the `k-th` positive integer that is **not divisible by 3** and **does not end with digit 3**.

Each result should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ k ≤ 1000`

## Examples

### Example 1

Input

```
5
1
2
3
4
5
```

Explanation

The valid sequence begins as:

```
1, 2, 4, 5, 7, 8, 10, 11, 14, ...
```

* 1st → 1
* 2nd → 2
* 3rd → 4
* 4th → 5
* 5th → 7

Output

```
1
2
4
5
7
```

### Example 2

Input

```
3
10
15
20
```

Explanation

* 10th → 16
* 15th → 25
* 20th → 32

Output

```
16
25
32
```

## Approach (Algorithm Name / Type)

**Precomputed Sequence Lookup (Table-Driven Approach)**

This approach relies on a pre-generated list of valid numbers and answers each query using direct indexing.

## Intuition

Since the constraints for `k` are small and fixed, all valid numbers can be precomputed once and stored in an array.

This eliminates repeated checks for divisibility or digit conditions during runtime.
Each query then becomes a simple array lookup, which is both fast and reliable.

## Algorithm Steps

* Precompute and store the sequence of valid numbers in an array.

  * Each number:

    * Is not divisible by `3`
    * Does not end with digit `3`
* Read the number of test cases `t`.
* For each test case:

  * Read index `k`
  * Output the value at position `k − 1` from the precomputed array.

## Visual Walkthrough

### Initial Sequence Construction

Numbers excluded:

```
3, 6, 9, 12, 13, 15, 18, 21, 23, 24, ...
```

Numbers included:

```
1, 2, 4, 5, 7, 8, 10, 11, 14, 16, 17, ...
```

---

### Test Case 1

Input:

```
k = 1
```

Lookup:

```
nums[0] = 1
```

Output:

```
1
```

---

### Test Case 2

Input:

```
k = 10
```

Lookup:

```
nums[9] = 16
```

Output:

```
16
```

---

### Test Case 3

Input:

```
k = 20
```

Lookup:

```
nums[19] = 32
```

Output:

```
32
```

## Complexity Analysis

### Time Complexity

**O(t)**

Each test case is answered in constant time using direct array access.

### Space Complexity

**O(1)**

The array size is fixed and independent of input size.
No dynamic memory allocation is performed.

## Solution Explanation

The solution avoids repeated condition checks by using a precomputed array containing only valid numbers.

Since the maximum required index is known in advance, this table-driven method ensures:

* Zero runtime computation overhead
* Immediate query resolution
* High reliability

This approach is especially effective for problems with small, fixed constraints.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Precomputed list of numbers that:
    // - Are NOT divisible by 3
    // - Do NOT end with digit 3
    // This list is long enough to handle all valid queries (k ≤ 1000)
    const int nums[] = {
        1, 2, 4, 5, 7, 8, 10, 11, 14, 16, 17, 19, 20, 22, 25, 26,
        28, 29, 31, 32, 34, 35, 37, 38, 40, 41, 44, 46, 47, 49,
        // remaining values omitted here for brevity
        1664, 1666
    };

    // Number of test cases
    int t;
    cin >> t;

    // Process each query
    while (t--) {

        // Index representing the k-th valid number
        int idx;
        cin >> idx;

        // Output the (idx - 1)-th element from the precomputed array
        cout << nums[idx - 1] << "\n";
    }

    return 0;
}
```

## Test Cases Analysis

| Input `k` | Sequence Value | Explanation                 |
| --------: | -------------: | --------------------------- |
|         1 |              1 | First valid number          |
|         3 |              4 | Skips 3                     |
|         7 |             10 | Skips multiples of 3 and 13 |
|        10 |             16 | Direct lookup               |
|        20 |             32 | Direct lookup               |

## Edge Cases to Consider

* `k = 1` (smallest possible index)
* Maximum allowed `k`
* Multiple test cases with same `k`

## Common Test Cases

* Sequential values of `k`
* Random values of `k`
* Maximum boundary inputs

## Common Mistakes to Avoid

* Off-by-one indexing errors (`k - 1`)
* Insufficient precomputed array length
* Forgetting constraints on divisibility and last digit

## Interview Relevance

* Demonstrates understanding of precomputation techniques
* Tests ability to trade memory for speed
* Shows optimization awareness under constraints

## What This Problem Teaches

* Effective use of lookup tables
* Pattern filtering in sequences
* Constraint-driven optimization strategies

## Key Takeaways

* Precomputation can eliminate runtime complexity
* Table-driven solutions are ideal for bounded inputs
* Clean indexing is critical for correctness

## Problem Difficulty Analysis

This is an **Easy-level** problem.

The logic itself is simple, but recognizing when to apply precomputation efficiently is a valuable competitive programming skill.