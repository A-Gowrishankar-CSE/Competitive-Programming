# A_I_Wanna_Be_the_Guy

## Platform

Codeforces

## Problem Link

[A. I Wanna Be the Guy](https://codeforces.com/problemset/problem/469/A)

## Problem Statement

There is a game consisting of `n` levels, numbered from `1` to `n`.

Two players, **Little X** and **Little Y**, are playing the game:

* Little X can pass some levels
* Little Y can pass some levels

To complete the game, **every level from `1` to `n` must be passed by at least one of them**.

Given the list of levels each player can pass, determine whether the game can be fully completed.

## Input Format

* The first line contains an integer `n` — the total number of levels
* The second line contains an integer `p` — the number of levels Little X can pass
  followed by `p` integers representing those levels
* The third line contains an integer `q` — the number of levels Little Y can pass
  followed by `q` integers representing those levels

## Output Format

* Print `"I become the guy."` if all levels can be passed
* Print `"Oh, my keyboard!"` otherwise

## Constraints

* `1 ≤ n ≤ 100`
* `0 ≤ p, q ≤ n`
* Level numbers are between `1` and `n`

## Examples

### Example 1

Input

```
4
3 1 2 3
2 2 4
```

Explanation

* Levels passed by Little X: 1, 2, 3
* Levels passed by Little Y: 2, 4
* All levels from 1 to 4 are covered

Output

```
I become the guy.
```

---

### Example 2

Input

```
5
1 1
1 3
```

Explanation

* Covered levels: 1 and 3
* Levels 2, 4, and 5 are missing

Output

```
Oh, my keyboard!
```

## Approach

**Level coverage tracking using a boolean array**

## Intuition

The objective is to verify whether **every level from `1` to `n` appears in at least one player’s list**.

A boolean array of size `n` can be used to track which levels are covered.
If any level remains uncovered after processing both players’ inputs, the game cannot be completed.

## Algorithm Steps

* Read the total number of levels `n`
* Initialize a boolean array of size `n` with all values set to `false`
* Read the number of levels `p` Little X can pass and mark them as covered
* Read the number of levels `q` Little Y can pass and mark them as covered
* Iterate through the boolean array:

  * If any level is not covered, print `"Oh, my keyboard!"` and terminate
* If all levels are covered, print `"I become the guy."`

## Visual Walkthrough

### Case 1

Input

```
n = 3
X: 1 2
Y: 3
```

Coverage tracking

```
Level 1 → covered
Level 2 → covered
Level 3 → covered
```

Result

```
I become the guy.
```

---

### Case 2

Input

```
n = 4
X: 1
Y: 3
```

Coverage tracking

```
Level 1 → covered
Level 2 → not covered
Level 3 → covered
Level 4 → not covered
```

Result

```
Oh, my keyboard!
```

---

### Case 3

Input

```
n = 1
X: (none)
Y: 1
```

Coverage tracking

```
Level 1 → covered
```

Result

```
I become the guy.
```

## Complexity Analysis

### Time Complexity

**O(n + p + q)**

* Reading and marking levels takes `O(p + q)`
* Final verification takes `O(n)`

### Space Complexity

**O(n)**

A boolean array of size `n` is used to track level coverage.

## Solution Explanation

The solution ensures correctness by:

* Marking every level that can be passed by either player
* Verifying complete coverage of all levels
* Using early termination when a missing level is detected

This approach is straightforward, efficient, and maps directly to the problem statement.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Total number of levels
    int n;
    cin >> n;

    // Boolean array to track covered levels
    bool f[n] = { false };

    // Levels passed by Little X
    int p;
    cin >> p;
    while (p--) {
        int level;
        cin >> level;
        f[level - 1] = true;
    }

    // Levels passed by Little Y
    int q;
    cin >> q;
    while (q--) {
        int level;
        cin >> level;
        f[level - 1] = true;
    }

    // Check if all levels are covered
    for (bool covered : f) {
        if (!covered) {
            cout << "Oh, my keyboard!\n";
            return 0;
        }
    }

    // All levels are covered
    cout << "I become the guy.\n";
    return 0;
}
```

## Test Cases Analysis

| n | X Levels | Y Levels | Output            |
| - | -------- | -------- | ----------------- |
| 4 | 1 2 3    | 2 4      | I become the guy. |
| 5 | 1        | 3        | Oh, my keyboard!  |
| 1 | —        | 1        | I become the guy. |
| 3 | 1 2 3    | —        | I become the guy. |

## Edge Cases to Consider

* One player passes no levels
* One player passes all levels
* Minimum value of `n`
* Overlapping level lists

## Common Test Cases

* Complete coverage using both players
* Incomplete coverage
* Single-level game

## Common Mistakes to Avoid

* Forgetting to convert levels to zero-based indexing
* Not checking all levels after input
* Assuming one player must cover all levels

## Interview Relevance

* Tests array usage and logical coverage checks
* Demonstrates clean handling of input aggregation
* Common introductory problem for competitive programming

## What This Problem Teaches

* Union of two sets using simple data structures
* Coverage verification techniques
* Early termination for efficiency

## Key Takeaways

* Boolean arrays are effective for fixed-range tracking
* Always verify complete coverage explicitly
* Simplicity leads to reliable solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on basic array usage and logical completeness checks, making it suitable for beginners and early interview practice.