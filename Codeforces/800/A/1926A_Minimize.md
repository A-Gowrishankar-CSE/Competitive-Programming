# A_Minimize

## Platform

Codeforces

## Problem Link

[A. Minimize](https://codeforces.com/problemset/problem/1926/A)

## Problem Statement

You are given multiple test cases.
In each test case, two integers `a` and `b` are provided such that `a ≤ b`.

Your task is to determine the **minimum value of the expression** when transforming `a` into `b` using the allowed operation defined by the problem.

For this specific problem, the required output is simply the **difference between `b` and `a`**.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each of the next `t` lines contains two integers `a` and `b`.

## Output Format

For each test case, print a single integer — the value of `b − a`.

Each result should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* `0 ≤ a ≤ b ≤ 10^9`

## Examples

### Example 1

Input

```
3
1 5
4 4
10 15
```

Explanation

* Test case 1: `5 − 1 = 4`
* Test case 2: `4 − 4 = 0`
* Test case 3: `15 − 10 = 5`

Output

```
4
0
5
```

### Example 2

Input

```
1
0 100
```

Explanation

* Difference between `b` and `a` is `100`

Output

```
100
```

## Approach (Algorithm Name / Type)

**Direct Arithmetic Difference Evaluation**

This approach computes the result using a simple subtraction operation.

## Intuition

To minimize the required value:

* The smallest achievable difference between `a` and `b` is obtained by directly subtracting `a` from `b`.

No loops, conditions, or additional logic are required because the problem guarantees valid input ordering.

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read integers `a` and `b`.
  * Compute `b − a`.
  * Print the result.

## Visual Walkthrough

### Test Case 1

Input:

```
a = 1, b = 5
```

Computation:

```
b − a = 5 − 1 = 4
```

Result:

```
4
```

---

### Test Case 2

Input:

```
a = 4, b = 4
```

Computation:

```
b − a = 0
```

Result:

```
0
```

---

### Test Case 3

Input:

```
a = 10, b = 15
```

Computation:

```
b − a = 5
```

Result:

```
5
```

## Complexity Analysis

### Time Complexity

**O(t)**

Each test case is processed in constant time.

### Space Complexity

**O(1)**

Only two integer variables are used per test case.

## Solution Explanation

The solution directly applies subtraction to compute the required result.

Since the input ensures `a ≤ b`, the subtraction always yields a non-negative value, and no additional checks are needed. This makes the solution optimal, readable, and efficient.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while (t--) {

        // Read the two integers
        int a, b;
        cin >> a >> b;

        // Output the difference
        cout << b - a << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Input (`a b`) | Calculation | Output |
| ------------- | ----------- | ------ |
| `1 5`         | `5 − 1`     | 4      |
| `4 4`         | `4 − 4`     | 0      |
| `10 15`       | `15 − 10`   | 5      |
| `0 100`       | `100 − 0`   | 100    |

## Edge Cases to Consider

* `a` equals `b`
* `a` is zero
* Large values of `b`

## Common Test Cases

* Identical values
* Small differences
* Large differences

## Common Mistakes to Avoid

* Reversing subtraction order (`a − b`)
* Forgetting to print a newline
* Overcomplicating a simple arithmetic problem

## Interview Relevance

* Tests understanding of basic arithmetic
* Evaluates ability to identify trivial solutions
* Common warm-up or screening question

## What This Problem Teaches

* Recognizing when a problem has a direct solution
* Avoiding unnecessary logic
* Writing clean and minimal code

## Key Takeaways

* Simple problems often require simple solutions
* Always analyze constraints before coding
* Direct arithmetic is often optimal

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It requires minimal reasoning and serves as a confidence-building task for beginners and quick assessments in competitive programming.