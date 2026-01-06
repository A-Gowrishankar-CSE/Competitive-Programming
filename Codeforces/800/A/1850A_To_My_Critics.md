# A_To_My_Critics

## Platform

Codeforces

## Problem Link

[A. To My Critics](https://codeforces.com/problemset/problem/1850/A)

## Problem Statement

You are given multiple test cases.
In each test case, three integers represent the scores given by three critics.

A performance is considered **successful** if **any two critics together give a total score of at least 10**.

Your task is to determine, for each test case, whether the performance is successful.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each of the next `t` lines contains three integers `a`, `b`, and `c`.

## Output Format

For each test case:

* Print `"YES"` if at least one pair of scores sums to `10` or more.
* Otherwise, print `"NO"`.

Each result should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* `0 ≤ a, b, c ≤ 10`

## Examples

### Example 1

Input

```
4
4 5 6
3 3 3
10 0 0
1 9 0
```

Explanation

* Test case 1: `5 + 6 = 11` → successful
* Test case 2: `3 + 3 = 6` → not successful
* Test case 3: `10 + 0 = 10` → successful
* Test case 4: `1 + 9 = 10` → successful

Output

```
YES
NO
YES
YES
```

### Example 2

Input

```
1
2 2 5
```

Explanation

* All pair sums are less than 10

Output

```
NO
```

## Approach (Algorithm Name / Type)

**Pairwise Sum Validation Using Conditional Checks**

This approach evaluates all possible pairs among three values to verify if any pair meets the required threshold.

## Intuition

There are exactly three possible pairs that can be formed from three numbers:

* `a + b`
* `b + c`
* `a + c`

If **any one** of these sums is at least `10`, the condition is satisfied.

Because the input size is very small and fixed, checking all pairs directly is the simplest and most reliable approach.

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read integers `a`, `b`, and `c`.
  * Check if:

    * `a + b ≥ 10`, or
    * `b + c ≥ 10`, or
    * `a + c ≥ 10`
  * If any condition is true, print `"YES"`.
  * Otherwise, print `"NO"`.

## Visual Walkthrough

### Test Case 1

Input:

```
a = 4, b = 5, c = 6
```

Pair sums:

```
a + b = 9
b + c = 11
a + c = 10
```

Decision:

```
At least one sum ≥ 10 → YES
```

---

### Test Case 2

Input:

```
a = 3, b = 3, c = 3
```

Pair sums:

```
3 + 3 = 6
3 + 3 = 6
3 + 3 = 6
```

Decision:

```
All sums < 10 → NO
```

---

### Test Case 3

Input:

```
a = 10, b = 0, c = 0
```

Pair sums:

```
10 + 0 = 10
```

Decision:

```
Sum ≥ 10 → YES
```

## Complexity Analysis

### Time Complexity

**O(t)**

Each test case performs a constant number of arithmetic operations and comparisons.

### Space Complexity

**O(1)**

Only a few integer variables are used.
No additional memory allocation is required.

## Solution Explanation

The solution explicitly checks all possible combinations of two critics’ scores.

Because there are only three values, the logic is clear, concise, and free of unnecessary complexity. The approach guarantees correctness by directly following the problem’s condition.

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

        // Scores given by three critics
        int a, b, c;
        cin >> a >> b >> c;

        // Check if any pair of scores sums to at least 10
        if (a + b >= 10 || b + c >= 10 || a + c >= 10) {
            cout << "YES\n";
        } else {
            cout << "NO\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Scores (`a b c`) | Pair Sums Checked | Result |
| ---------------- | ----------------- | ------ |
| `4 5 6`          | `5+6 = 11`        | YES    |
| `3 3 3`          | All < 10          | NO     |
| `10 0 0`         | `10+0 = 10`       | YES    |
| `2 2 5`          | All < 10          | NO     |

## Edge Cases to Consider

* Exactly one pair summing to `10`
* All scores being zero
* One score being maximum and others minimum

## Common Test Cases

* Mixed small and large values
* Symmetric values (`a = b = c`)
* One dominating score

## Common Mistakes to Avoid

* Checking only one pair instead of all three
* Using `>` instead of `≥`
* Printing incorrect output format (`Yes` instead of `YES`)

## Interview Relevance

* Tests conditional logic and completeness
* Evaluates ability to consider all combinations
* Common warm-up problem in coding interviews

## What This Problem Teaches

* Exhaustive checking for small fixed input sizes
* Translating real-world rules into program logic
* Writing clear and maintainable conditional statements

## Key Takeaways

* Always consider all possible combinations
* Simplicity is often the best solution
* Fixed-size inputs allow direct and readable logic

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on basic arithmetic and logical reasoning, making it suitable for beginners and quick interview assessments.