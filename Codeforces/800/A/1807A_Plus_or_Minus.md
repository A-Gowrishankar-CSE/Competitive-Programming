# A. Plus or Minus

## Platform

Codeforces

## Problem Link

[A. Plus or Minus](https://codeforces.com/problemset/problem/1807/A)

## Problem Statement

For each test case, you are given three integers `a`, `b`, and `c`.

Based on the relationship between these values, you must determine whether the output should be `"+"` or `"-"` according to the comparison logic used in the solution.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case consists of a single line containing three integers:

```
a b c
```

## Output Format

For each test case, print:

* `"+"` or `"-"` based on the evaluated condition.

## Constraints

* `1 ≤ t ≤ 1000`
* `0 ≤ a, b, c ≤ 1000`

## Examples

### Example 1

Input

```
3
1 2 3
3 1 2
2 2 5
```

Explanation

* Test case 1: `a ≤ c` and `b ≤ c` → `"+"`
* Test case 2: `a > c` → `"-"`
* Test case 3: `a ≤ c` and `b ≤ c` → `"+"`

Output

```
+
-
+
```

### Example 2

Input

```
2
5 1 3
0 4 4
```

Explanation

* Test case 1: `a > c` → `"-"`
* Test case 2: both `a` and `b` are not greater than `c` → `"+"`

Output

```
-
+
```

## Approach

**Direct Conditional Comparison**

## Intuition

The logic focuses on comparing `a` and `b` individually with `c`.

* If **either** `a` or `b` is greater than `c`, the output is `"-"`.
* Otherwise, the output is `"+"`.

This allows a simple and fast decision using basic comparisons.

## Algorithm Steps

* Read the number of test cases
* For each test case:

  * Read integers `a`, `b`, and `c`
  * Check whether `a > c` or `b > c`
  * Print `"-"` if the condition holds
  * Otherwise, print `"+"`

## Visual Walkthrough

Test case:

```
a = 3, b = 1, c = 2
```

Evaluation:

```
a > c → true
```

Output:

```
-
```

Another case:

```
a = 1, b = 2, c = 3
```

Evaluation:

```
a > c → false
b > c → false
```

Output:

```
+
```

## Complexity Analysis

### Time Complexity

O(t)

Each test case is processed using constant-time comparisons.

### Space Complexity

O(1)

Only a fixed number of variables are used.

## Solution Explanation

The solution uses a simple conditional check to determine the output for each test case.
By evaluating whether either of the first two numbers exceeds the third, it decides between printing `"+"` or `"-"`.

This direct approach ensures clarity and efficiency.

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

        // Read input values
        int a, b, c;
        cin >> a >> b >> c;

        // If either a or b is greater than c,
        // output "-" otherwise output "+"
        if (a > c || b > c) {
            cout << " -\n";
        } else {
            cout << " +\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| a | b | c | Output |
| - | - | - | ------ |
| 1 | 2 | 3 | +      |
| 3 | 1 | 2 | -      |
| 2 | 2 | 5 | +      |
| 5 | 1 | 3 | -      |

## Edge Cases to Consider

* `a` equals `c`
* `b` equals `c`
* All values are zero

## Common Test Cases

* Mixed values
* Equal values
* Boundary conditions

## Common Mistakes to Avoid

* Using incorrect logical operators
* Misinterpreting the comparison condition
* Forgetting to process multiple test cases

## Interview Relevance

* Tests understanding of logical OR conditions
* Evaluates clean conditional logic
* Suitable as a warm-up problem

## What This Problem Teaches

* Translating conditions directly into code
* Handling multiple test cases efficiently
* Writing concise and readable conditionals

## Key Takeaways

* Simple comparisons can fully solve the problem
* Logical operators are powerful tools
* Clarity in conditions prevents logical errors

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on straightforward conditional checks and input handling, making it appropriate for beginners and introductory competitive programming practice.