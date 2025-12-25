# A_Divisibility_Problem

## Platform

Codeforces

## Problem Link

[A. Divisibility Problem](https://codeforces.com/problemset/problem/1328/A)

## Problem Statement

You are given multiple test cases.
For each test case, two integers `a` and `b` are provided.

Your task is to determine the **minimum non-negative integer `x`** such that:

```
(a + x) is divisible by b
```

In other words, you must find how much needs to be added to `a` so that it becomes a multiple of `b`.

## Input Format

* The first line contains an integer `t` — the number of test cases
* Each of the next `t` lines contains two integers `a` and `b`

## Output Format

* For each test case, print a single integer
  The minimum value of `x`

## Constraints

* `1 ≤ t ≤ 10^4`
* `1 ≤ a, b ≤ 10^9`

## Examples

### Example 1

Input

```
3
10 4
13 9
100 10
```

Explanation

* `10` is already divisible by `4` → add `0`
* `13 % 9 = 4` → need to add `5`
* `100` is already divisible by `10` → add `0`

Output

```
0
5
0
```

---

### Example 2

Input

```
1
7 5
```

Explanation

```
7 % 5 = 2
Next multiple of 5 is 10
10 - 7 = 3
```

Output

```
3
```

## Approach

**Modulo-based arithmetic adjustment**

## Intuition

If `a` is already divisible by `b`, the answer is `0`.

Otherwise, the remainder `a % b` tells us how far `a` is from the **previous multiple** of `b`.
To reach the **next multiple**, we must add:

```
b - (a % b)
```

The additional modulo operation ensures the result is `0` when `a` is already divisible by `b`.

## Algorithm Steps

* Read the number of test cases `t`
* For each test case:

  * Read integers `a` and `b`
  * Compute `a % b`
  * Calculate the required addition using
    `(b - a % b) % b`
  * Print the result

## Visual Walkthrough

### Case 1

Input

```
a = 10, b = 4
```

Calculation

```
10 % 4 = 2
4 - 2 = 2
```

Result

```
2
```

---

### Case 2

Input

```
a = 12, b = 4
```

Calculation

```
12 % 4 = 0
(4 - 0) % 4 = 0
```

Result

```
0
```

---

### Case 3

Input

```
a = 13, b = 9
```

Calculation

```
13 % 9 = 4
9 - 4 = 5
```

Result

```
5
```

## Complexity Analysis

### Time Complexity

**O(t)**

Each test case is processed in constant time using arithmetic operations.

### Space Complexity

**O(1)**

Only a fixed number of variables are used per test case.

## Solution Explanation

The solution relies entirely on **modulo arithmetic**.

The expression:

```
(b - a % b) % b
```

works correctly in all cases:

* If `a` is already divisible by `b`, the result is `0`
* Otherwise, it computes the exact amount needed to reach the next multiple of `b`

This avoids conditional branching and keeps the implementation concise and efficient.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while (t--) {

        // Read values a and b
        int a, b;
        cin >> a >> b;

        // Compute the minimum value to add to 'a'
        // so that (a + x) becomes divisible by 'b'
        cout << (b - a % b) % b << endl;
    }

    return 0;
}
```

## Test Cases Analysis

| a  | b | a % b | Output |
| -- | - | ----- | ------ |
| 10 | 4 | 2     | 2      |
| 12 | 4 | 0     | 0      |
| 13 | 9 | 4     | 5      |
| 7  | 5 | 2     | 3      |

## Edge Cases to Consider

* `a` already divisible by `b`
* Very large values of `a` and `b`
* `b` greater than `a`

## Common Test Cases

* `(a, b)` where `a % b == 0`
* `(a, b)` where `a < b`
* Large number of test cases

## Common Mistakes to Avoid

* Forgetting to handle the case when `a % b == 0`
* Using conditional checks instead of clean modulo logic
* Printing negative values due to incorrect subtraction

## Interview Relevance

* Tests understanding of modulo arithmetic
* Demonstrates clean mathematical reasoning
* Frequently used in competitive programming warm-ups

## What This Problem Teaches

* Effective use of modulo operations
* Eliminating conditionals through mathematical expressions
* Writing concise and robust logic

## Key Takeaways

* Modulo arithmetic simplifies divisibility problems
* Small mathematical tricks can eliminate branching
* Always consider edge cases like exact divisibility

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on arithmetic reasoning rather than algorithmic complexity and is ideal for beginners and interview preparation.