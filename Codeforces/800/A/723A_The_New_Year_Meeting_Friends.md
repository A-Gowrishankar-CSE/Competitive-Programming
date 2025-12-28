# A_The_New_Year_Meeting_Friends

## Platform

Codeforces

## Problem Link

[A. The New Year Meeting Friends](https://codeforces.com/problemset/problem/723/A)

## Problem Statement

Three friends want to meet at a single point on a number line to celebrate the New Year.

Each friend is located at a different integer coordinate.
They want to choose a meeting point such that the **total distance** traveled by all three friends is **minimized**.

Your task is to calculate this **minimum total distance**.

## Input Format

* A single line containing three integers `a`, `b`, and `c` — the coordinates of the three friends

## Output Format

* Print one integer — the minimum total distance

## Constraints

* `0 ≤ a, b, c ≤ 100`

## Examples

### Example 1

Input

```
1 2 3
```

Explanation

The optimal meeting point is `2`.

Total distance:

```
|2 − 1| + |2 − 2| + |2 − 3| = 2
```

Output

```
2
```

---

### Example 2

Input

```
4 7 1
```

Explanation

The optimal meeting point is `4`.

Total distance:

```
|4 − 4| + |4 − 7| + |4 − 1| = 6
```

Output

```
6
```

---

### Example 3

Input

```
10 0 0
```

Explanation

The optimal meeting point is `0`.

Total distance:

```
|0 − 10| + |0 − 0| + |0 − 0| = 10
```

Output

```
10
```

## Approach

**Selecting the median of three values**

## Intuition

On a number line, the point that minimizes the sum of absolute distances is the **median**.

For three values:

* The **middle value** (after ordering) always minimizes total travel distance.

The solution therefore finds the middle value among `a`, `b`, and `c` and computes the total distance to that point.

## Algorithm Steps

* Read integers `a`, `b`, and `c`
* Determine which value lies between the other two (the median)
* Calculate:

  ```
  |mid − a| + |mid − b| + |mid − c|
  ```
* Output the result

## Visual Walkthrough

### Case 1

Input

```
1 2 3
```

Median

```
2
```

Distance

```
1 + 0 + 1 = 2
```

---

### Case 2

Input

```
7 1 4
```

Median

```
4
```

Distance

```
3 + 0 + 3 = 6
```

---

### Case 3

Input

```
5 5 1
```

Median

```
5
```

Distance

```
0 + 0 + 4 = 4
```

## Complexity Analysis

### Time Complexity

**O(1)**

Only a fixed number of comparisons and arithmetic operations are performed.

### Space Complexity

**O(1)**

No extra data structures are used.

## Solution Explanation

The solution identifies the median without sorting by using pairwise comparisons.

Once the median is determined, computing the sum of absolute differences gives the minimum total distance.

This approach is efficient and mathematically optimal for minimizing absolute distance on a line.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    int a, b, c, mid;
    cin >> a >> b >> c;

    // Determine the median value
    if ((a > b && a < c) || (a < b && a > c))
        mid = a;
    else if ((b > a && b < c) || (b < a && b > c))
        mid = b;
    else
        mid = c;

    // Calculate and print the minimum total distance
    cout << abs(mid - a) + abs(mid - b) + abs(mid - c);

    return 0;
}
```

## Test Cases Analysis

| a | b | c  | Output |
| - | - | -- | ------ |
| 1 | 2 | 3  | 2      |
| 4 | 7 | 1  | 6      |
| 0 | 0 | 10 | 10     |
| 5 | 5 | 5  | 0      |

## Edge Cases to Consider

* Two or all coordinates are the same
* Coordinates are already in sorted order
* Coordinates are in reverse order
* Extreme values within constraints

## Common Mistakes to Avoid

* Choosing the average instead of the median
* Forgetting absolute values
* Overcomplicating the solution with sorting

## Interview Relevance

* Tests understanding of medians
* Evaluates mathematical reasoning
* Common optimization problem

## What This Problem Teaches

* Why the median minimizes absolute distance
* Efficient comparison-based logic
* Avoiding unnecessary sorting

## Key Takeaways

* For absolute distance minimization, always choose the median
* Sorting is not required for only three elements
* Simple comparisons can yield optimal results

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on fundamental mathematical reasoning and conditional logic, making it ideal for beginners and early competitive programming practice.