# A. Marathon

## Platform

Codeforces

## Problem Link

[A. Marathon](https://codeforces.com/problemset/problem/1692/A)

## Problem Statement

Four runners participate in a marathon.

* The first runner finishes in time `a`
* The other three runners finish in times `b`, `c`, and `d`

A runner is considered **faster** if their finishing time is **strictly less**.

Determine how many of the other three runners finished **faster than the first runner**.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case consists of a single line containing four integers:

```
a b c d
```

## Output Format

For each test case, print a single integer representing the count of runners who finished faster than the first runner.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ a, b, c, d ≤ 10^4`

## Examples

### Example 1

Input

```
3
10 9 8 11
5 6 7 8
100 100 100 100
```

Explanation

* Test case 1: `b` and `c` are faster than `a` → `2`
* Test case 2: all runners are slower → `0`
* Test case 3: all finish at the same time → `0`

Output

```
2
0
0
```

### Example 2

Input

```
1
7 6 5 4
```

Explanation
All three runners finished faster than the first runner.

Output

```
3
```

## Approach

**Direct Comparison Counting**

## Intuition

Only the finishing time of the first runner matters.
Each of the remaining three times is compared independently against `a`.

If a runner’s time is strictly less than `a`, they are faster.

## Algorithm Steps

* Read the number of test cases
* For each test case:

  * Read `a`, `b`, `c`, and `d`
  * Initialize a counter
  * Compare `b`, `c`, and `d` with `a`
  * Increment the counter for each faster runner
  * Output the counter

## Visual Walkthrough

Test case:

```
a = 10, b = 9, c = 8, d = 11
```

Comparisons:

```
b < a → faster
c < a → faster
d > a → slower
```

Total faster runners:

```
2
```

Another case:

```
a = 5, b = 6, c = 7, d = 8
```

All runners are slower → `0`.

## Complexity Analysis

### Time Complexity

O(t)

Each test case performs a constant number of comparisons.

### Space Complexity

O(1)

Only constant extra variables are used.

## Solution Explanation

The solution checks each of the three competitors against the first runner’s time.
By using simple conditional comparisons, it counts how many runners finished faster and prints the result.

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

        // Finishing times of runners
        int a, b, c, d;
        cin >> a >> b >> c >> d;

        // Counter for runners faster than the first runner
        int count = 0;

        // Compare each runner's time with the first runner
        if (b < a) count++;
        if (c < a) count++;
        if (d < a) count++;

        // Output the result
        cout << count << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| a   | b   | c   | d   | Faster Runners |
| --- | --- | --- | --- | -------------- |
| 10  | 9   | 8   | 11  | 2              |
| 5   | 6   | 7   | 8   | 0              |
| 7   | 6   | 5   | 4   | 3              |
| 100 | 100 | 100 | 100 | 0              |

## Edge Cases to Consider

* All runners have the same time
* All runners are faster
* All runners are slower

## Common Test Cases

* Mixed finishing times
* Equal values
* Boundary values

## Common Mistakes to Avoid

* Using `<=` instead of `<`
* Forgetting to reset the counter per test case
* Misinterpreting “faster” as greater time

## Interview Relevance

* Tests conditional logic
* Evaluates clarity in comparisons
* Typical beginner-level problem

## What This Problem Teaches

* Precise interpretation of problem statements
* Clean and direct comparison logic
* Handling multiple test cases

## Key Takeaways

* Always confirm comparison direction
* Keep logic minimal and readable
* Constant-time solutions are often enough

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It emphasizes correct interpretation and simple condition checks, making it suitable for beginners and competitive programming warm-ups.