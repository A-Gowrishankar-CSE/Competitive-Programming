# A. Domino Piling

## Platform

Codeforces

## Problem Link

[A. Domino Piling](https://codeforces.com/problemset/problem/50/A)

## Problem Statement

You are given a rectangular board of size `m × n`.
You want to place as many **2 × 1 dominoes** on the board as possible.

Each domino covers exactly two adjacent cells, and dominoes **cannot overlap** or extend outside the board.

Determine the **maximum number of dominoes** that can be placed on the board.

## Input Format

* A single line containing two integers `m` and `n`.

## Output Format

* Print a single integer representing the maximum number of dominoes that can be placed.

## Constraints

* `1 ≤ m, n ≤ 16`

## Examples

### Example 1

Input

```
2 4
```

Explanation
The board has:

```
2 × 4 = 8 cells
```

Each domino covers `2` cells.

Maximum dominoes:

```
8 / 2 = 4
```

Output

```
4
```

---

### Example 2

Input

```
3 3
```

Explanation
Total cells:

```
3 × 3 = 9
```

Since each domino needs 2 cells:

```
9 / 2 = 4 (integer division)
```

One cell remains unused.

Output

```
4
```

---

## Approach

Mathematical greedy approach using area calculation.

## Intuition

* A domino always occupies exactly **two cells**.
* The board contains `m × n` cells in total.
* The maximum number of dominoes is simply the number of cell pairs available.

No matter how the dominoes are placed (horizontally or vertically), the **maximum count depends only on total area**, not on orientation.

## Algorithm Steps

* Read the values `m` and `n`
* Compute the total number of cells: `m × n`
* Divide the total cell count by `2`
* Output the result

## Visual Walkthrough

For a `3 × 4` board:

```
Total cells = 12
Each domino = 2 cells
```

Domino placement count:

```
12 / 2 = 6
```

Even if the board dimensions are odd, integer division ensures only complete dominoes are counted.

## Complexity Analysis

### Time Complexity

O(1)
Only a single arithmetic calculation is performed.

### Space Complexity

O(1)
No additional memory is used.

## Solution Explanation

The solution calculates the total number of cells on the board and divides it by two since each domino occupies exactly two cells.
Using integer division automatically handles cases where one cell remains uncovered.

This approach is optimal, efficient, and directly follows the mathematical nature of the problem.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Dimensions of the board
    int m, n;

    // Read number of rows (m) and columns (n)
    cin >> m >> n;

    // Total number of cells is m * n
    // Each domino covers exactly 2 cells
    // Using integer division gives the maximum number of dominoes
    cout << (m * n) / 2;

    return 0;
}
```

## Test Cases Analysis

| Input | Total Cells | Calculation | Output |
| ----- | ----------- | ----------- | ------ |
| 2 2   | 4           | 4 / 2       | 2      |
| 2 3   | 6           | 6 / 2       | 3      |
| 3 3   | 9           | 9 / 2       | 4      |
| 1 5   | 5           | 5 / 2       | 2      |

## Edge Cases to Consider

* One row or one column
* Odd number of total cells
* Minimum board size (`1 × 1`)

## Common Test Cases

* Even-sized boards
* Odd-sized boards
* Single-row or single-column boards

## Common Mistakes to Avoid

* Trying to simulate placements instead of using math
* Forgetting integer division behavior
* Overcomplicating a simple arithmetic problem

## Interview Relevance

* Tests problem simplification skills
* Demonstrates mathematical reasoning
* Common example of greedy optimization

## What This Problem Teaches

* How to reduce a placement problem to a formula
* Importance of recognizing constraints early
* Avoiding unnecessary loops or simulations

## Key Takeaways

* Area-based reasoning can simplify many grid problems
* Integer division is crucial when only full units are allowed
* Simple logic often yields optimal solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on logical simplification and mathematical insight rather than implementation complexity, making it ideal for beginners and interview warm-up practice.