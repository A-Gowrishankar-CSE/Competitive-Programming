# A_Arrival_of_the_General

## Platform

Codeforces

## Problem Link

[A. Arrival of the General](https://codeforces.com/problemset/problem/144/A)

## Problem Statement

A line of soldiers is standing in a row. Each soldier has a certain height.

The general wants the **tallest soldier to stand at the beginning of the line** and the **shortest soldier to stand at the end of the line**.

In one move, you can swap **two adjacent soldiers**.

Your task is to determine the **minimum number of moves** required to achieve this arrangement.

Important details:

* If there are multiple tallest soldiers, choose the one **closest to the beginning**
* If there are multiple shortest soldiers, choose the one **closest to the end**

## Input Format

* The first line contains an integer `n` — the number of soldiers
* The second line contains `n` integers representing the heights of the soldiers

## Output Format

* Print a single integer — the minimum number of moves required

## Constraints

* `1 ≤ n ≤ 100`
* `1 ≤ height ≤ 100`

## Examples

### Example 1

Input

```
4
33 44 11 22
```

Explanation

* Tallest soldier: `44` at index `1`
* Shortest soldier: `11` at index `2`

Moves required:

* Move `44` to the front → `1` move
* Move `11` to the end → `1` move

Total moves = `2`

Output

```
2
```

---

### Example 2

Input

```
7
10 10 58 31 63 40 76
```

Explanation

* Tallest soldier: `76` at index `6`
* Shortest soldier: `10` at index `1` (last occurrence)

Moves required:

* Move `76` to the front → `6` moves
* Move `10` to the end → `5` moves

One overlap adjustment is required.

Output

```
10
```

## Approach

**Index tracking and swap count calculation**

## Intuition

Each adjacent swap moves a soldier **one position** left or right.

So:

* Moving the tallest soldier to the front requires `maxIdx` swaps
* Moving the shortest soldier to the end requires
  `n - minIdx - 1` swaps

However, if the tallest soldier is originally **to the right of** the shortest soldier, moving the tallest first shifts the shortest soldier one position left.
In this case, **one extra swap is counted**, so it must be subtracted.

## Algorithm Steps

* Read the number of soldiers `n`
* Traverse the heights:

  * Track the **first occurrence of the maximum height**
  * Track the **last occurrence of the minimum height**
* Compute:

  * Moves to bring tallest to front → `maxIdx`
  * Moves to bring shortest to end → `n - minIdx - 1`
* If `maxIdx > minIdx`, subtract `1`
* Output the final count

## Visual Walkthrough

### Case 1

Input

```
33 44 11 22
```

Indexes

```
44 → index 1
11 → index 2
```

Moves

```
Tallest to front → 1
Shortest to end → 1
```

Total

```
2
```

---

### Case 2

Input

```
5 1 3 4 1
```

Indexes

```
Tallest (5) → index 0
Shortest (1, last) → index 4
```

Moves

```
0 + 0 = 0
```

Result

```
0
```

---

### Case 3

Input

```
2 1 3
```

Indexes

```
Tallest → index 2
Shortest → index 1
```

Overlap adjustment applies.

## Complexity Analysis

### Time Complexity

**O(n)**

The list of soldiers is traversed once to find the required indices.

### Space Complexity

**O(1)**

Only a fixed number of variables are used.

## Solution Explanation

The solution efficiently calculates the minimum number of swaps by:

* Tracking the positions of the relevant soldiers during input
* Using direct index-based calculations instead of simulating swaps
* Correcting for overlapping movement when necessary

This avoids unnecessary operations while guaranteeing correctness.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of soldiers
    int n;
    cin >> n;

    // Track maximum and minimum heights and their indices
    int maxi = 0, mini = 100;
    int maxIdx = 0, minIdx = 0;

    // Read heights and update indices
    for (int i = 0; i < n; i++) {
        int height;
        cin >> height;

        // First occurrence of maximum
        if (height > maxi) {
            maxi = height;
            maxIdx = i;
        }

        // Last occurrence of minimum
        if (height <= mini) {
            mini = height;
            minIdx = i;
        }
    }

    // Calculate total moves
    cout << maxIdx + (n - minIdx - 1) - (maxIdx > minIdx) << endl;

    return 0;
}
```

## Test Cases Analysis

| Heights     | Max Index | Min Index | Output |
| ----------- | --------- | --------- | ------ |
| 33 44 11 22 | 1         | 2         | 2      |
| 5 1 3 4 1   | 0         | 4         | 0      |
| 1 2 3       | 2         | 0         | 2      |
| 10 10 10    | 0         | 2         | 0      |

## Edge Cases to Consider

* Tallest already at the front
* Shortest already at the end
* Multiple tallest or shortest soldiers
* Single soldier (`n = 1`)

## Common Test Cases

* Distinct heights
* Repeated heights
* Sorted and reverse-sorted inputs

## Common Mistakes to Avoid

* Choosing the wrong occurrence of minimum or maximum
* Forgetting the overlap adjustment
* Simulating swaps unnecessarily

## Interview Relevance

* Tests array traversal and index tracking
* Demonstrates optimization without simulation
* Common problem involving positional reasoning

## What This Problem Teaches

* How to reduce a swapping problem to index math
* Handling tie-breaking rules correctly
* Identifying overlap effects in movement problems

## Key Takeaways

* Direct calculations are often better than simulation
* Tie-breaking rules matter in problem statements
* Always account for side effects of earlier operations

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It requires careful observation and index-based reasoning rather than complex algorithms, making it a strong foundational competitive programming exercise.