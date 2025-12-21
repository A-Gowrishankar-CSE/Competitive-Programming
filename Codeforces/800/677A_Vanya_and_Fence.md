# A. Vanya and Fence

## Platform

Codeforces

## Problem Link

[A. Vanya and Fence](https://codeforces.com/problemset/problem/677/A)

## Problem Statement

Vanya and his friends are walking along a fence of height `k`.

There are `n` friends, each having a certain height.
To walk in a row:

* If a friend's height is **less than or equal to `k`**, they occupy **1 unit** of width.
* If a friend's height is **greater than `k`**, they must bend down and occupy **2 units** of width.

Determine the **minimum width of the road** required so that all friends can walk in a single row.

## Input Format

* The first line contains two integers `n` and `k`
* The second line contains `n` integers representing the heights of the friends

## Output Format

Print a single integer representing the total width required.

## Constraints

* `1 ≤ n ≤ 1000`
* `1 ≤ k ≤ 1000`
* `1 ≤ height[i] ≤ 1000`

## Examples

### Example 1

Input

```
3 7
4 5 14
```

Explanation

* Height 4 ≤ 7 → width = 1
* Height 5 ≤ 7 → width = 1
* Height 14 > 7 → width = 2

Total width = `1 + 1 + 2 = 4`

Output

```
4
```

### Example 2

Input

```
6 1
1 2 3 4 5 6
```

Explanation

* Height 1 ≤ 1 → width = 1
* Heights 2–6 > 1 → each occupies 2 units

Total width = `1 + 2×5 = 11`

Output

```
11
```

## Approach

Greedy counting based on height comparison.

Each friend is processed independently, and their contribution to the total width is added immediately.

## Intuition

Every friend contributes **at least 1 unit** of width.

If a friend is taller than the fence height `k`, they need **one additional unit**, making their total contribution **2 units**.

Thus:

* Always add `1` for each friend
* Add one more unit only when height exceeds `k`

## Algorithm Steps

* Read `n` and `k`
* Initialize a variable `width` to `0`
* For each friend:

  * Read height
  * If height is greater than `k`, increment `width` by 1
  * Increment `width` by 1 for the base width
* Output the final value of `width`

## Visual Walkthrough

Fence height: `k = 5`
Friend heights: `3 6 4`

```
Friend 1: height 3 ≤ 5 → width = 1
Friend 2: height 6 > 5 → width = 2
Friend 3: height 4 ≤ 5 → width = 1
```

Total width:

```
1 + 2 + 1 = 4
```

## Complexity Analysis

### Time Complexity

**O(n)**
Each friend is processed exactly once.

### Space Complexity

**O(n)**
An array is used to store heights.

## Solution Explanation

The solution iterates through the list of friend heights and calculates the required width incrementally.

For every friend, one unit of width is always added.
If a friend's height exceeds the fence height, one additional unit is added.

This direct counting approach avoids unnecessary computations and matches the problem constraints efficiently.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of friends and height of the fence
    int n, k;
    cin >> n >> k;

    // Array to store heights of friends
    int heights[n];

    // Variable to store total width required
    int width = 0;

    // Read heights and calculate width
    for (int i = 0; i < n; i++) {

        cin >> heights[i];

        // If friend's height is greater than fence,
        // they require extra width
        if (heights[i] > k)
            width++;

        // Every friend occupies at least 1 unit of width
        width++;
    }

    // Output the total width
    cout << width << endl;

    return 0;
}
```

## Test Cases Analysis

| n | k | Heights     | Expected Output |
| - | - | ----------- | --------------- |
| 3 | 7 | 4 5 14      | 4               |
| 1 | 5 | 10          | 2               |
| 5 | 3 | 1 2 3 4 5   | 7               |
| 6 | 1 | 1 2 3 4 5 6 | 11              |

## Edge Cases to Consider

* All friends taller than the fence
* All friends shorter than or equal to the fence
* Minimum input size (`n = 1`)

## Common Test Cases

* Mixed heights
* Uniform heights
* Extreme fence height values

## Common Mistakes to Avoid

* Forgetting to add the base width for each friend
* Misinterpreting width as height
* Incorrect condition (`>= k` instead of `> k`)

## Interview Relevance

* Tests conditional logic
* Reinforces greedy counting techniques
* Common beginner-level screening problem

## What This Problem Teaches

* Translating word problems into arithmetic logic
* Efficient iteration and counting
* Importance of interpreting constraints carefully

## Key Takeaways

* Every entity contributes a minimum cost
* Additional conditions add incremental cost
* Simple logic can be highly effective

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on condition checks and accumulation logic, making it suitable for beginners and early interview preparation.
