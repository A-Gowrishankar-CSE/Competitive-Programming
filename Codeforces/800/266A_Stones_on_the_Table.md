# A. Stones on the Table

## Platform

Codeforces

## Problem Link

[A. Stones on the Table](https://codeforces.com/problemset/problem/266/A)

## Problem Statement

There are `n` stones placed in a row.
Each stone is colored either **Red (`R`)**, **Green (`G`)**, or **Blue (`B`)**.

The stones are considered **beautiful** if no two adjacent stones have the same color.

Determine the **minimum number of stones that must be removed** so that the remaining stones are beautiful.

## Input Format

* The first line contains an integer `n`, the number of stones.
* The second line contains a string `s` of length `n`, representing the colors of the stones.

## Output Format

* Print a single integer representing the minimum number of stones to remove.

## Constraints

* `1 ≤ n ≤ 50`
* `s[i] ∈ { 'R', 'G', 'B' }`

## Examples

### Example 1

Input

```
3
RRG
```

Explanation
The first two stones are both `R`, so one must be removed.

Output

```
1
```

---

### Example 2

Input

```
5
RRGGB
```

Explanation
Adjacent equal-color pairs:

* `R R`
* `G G`

Minimum removals required:

```
2
```

Output

```
2
```

---

## Approach

Single-pass adjacent comparison.

## Intuition

* A stone only needs to be removed when it has the **same color as its immediate neighbor**.
* By counting how many times two adjacent stones are identical, we directly obtain the number of removals needed.

## Algorithm Steps

* Read the number of stones `n`
* Read the color string `s`
* Traverse the string from index `1` to `n-1`
* Compare each stone with its previous stone
* Increment a counter whenever two adjacent stones have the same color
* Output the counter

## Visual Walkthrough

Input:

```
R R G G B
```

Comparison:

```
R == R → remove 1
R != G → ok
G == G → remove 1
G != B → ok
```

Total removals:

```
2
```

## Complexity Analysis

### Time Complexity

O(n)
Each stone is checked once.

### Space Complexity

O(1)
Only a counter variable is used.

## Solution Explanation

The solution iterates through the string once, comparing each stone’s color with the color of the stone immediately before it.
Every time two adjacent stones have the same color, one of them must be removed to maintain the beauty condition.

The total count of such adjacent matches is the minimum number of stones to remove.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of stones
    int n;

    // Counter to track adjacent stones with the same color
    int neighbors = 0;

    // Read number of stones
    cin >> n;

    // String representing stone colors
    string s;
    cin >> s;

    // Traverse the string starting from the second character
    for (int i = 1; i < n; i++) {

        // If current stone has the same color as the previous one,
        // one stone must be removed
        if (s[i - 1] == s[i]) {
            neighbors++;
        }
    }

    // Output the minimum number of stones to remove
    cout << neighbors << endl;

    return 0;
}
```

## Test Cases Analysis

| Input   | Adjacent Matches | Output |
| ------- | ---------------- | ------ |
| `RGB`   | 0                | 0      |
| `RR`    | 1                | 1      |
| `RRGGB` | 2                | 2      |
| `BBBB`  | 3                | 3      |

## Edge Cases to Consider

* Only one stone
* All stones have the same color
* No two stones share the same color

## Common Test Cases

* Alternating colors
* Repeated colors in blocks
* Fully uniform color string

## Common Mistakes to Avoid

* Comparing non-adjacent stones
* Removing more stones than necessary
* Off-by-one errors in loop indexing

## Interview Relevance

* Tests string traversal and adjacency logic
* Reinforces greedy counting strategy
* Common beginner problem in interviews

## What This Problem Teaches

* Efficient handling of adjacency conditions
* Translating problem constraints directly into logic
* Avoiding unnecessary removals

## Key Takeaways

* Only adjacent comparisons matter
* Counting conflicts is often simpler than simulating removals
* Single-pass solutions are both efficient and clear

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It emphasizes string traversal and greedy counting, making it ideal for beginners and competitive programming practice.