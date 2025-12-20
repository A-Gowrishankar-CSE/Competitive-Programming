# A. Elephant

## Platform

Codeforces

## Problem Link

[A. Elephant](https://codeforces.com/problemset/problem/617/A)

## Problem Statement

An elephant wants to reach his friend who lives at position `x` on a number line.

The elephant starts at position `0`.
In one move, the elephant can move forward by **1, 2, 3, 4, or 5** positions.

Determine the **minimum number of moves** required for the elephant to reach exactly position `x`.

## Input Format

* A single integer `x` representing the destination position.

## Output Format

* Print a single integer representing the minimum number of moves required.

## Constraints

* `1 ≤ x ≤ 1,000,000`

## Examples

### Example 1

Input

```
5
```

Explanation
The elephant can move `5` units in one step.

Output

```
1
```

---

### Example 2

Input

```
12
```

Explanation
Optimal movement:

```
5 + 5 + 2 = 12
```

Total moves:

```
3
```

Output

```
3
```

---

## Approach

Greedy mathematical calculation.

## Intuition

* To minimize the number of moves, the elephant should always take the **largest possible step**.
* Since the maximum step size is `5`, the problem reduces to dividing `x` by `5`.
* If `x` is not divisible by `5`, one additional move is required.

## Algorithm Steps

* Read the value `x`
* Divide `x` by `5`
* If there is a remainder, add `1`
* Output the result

## Visual Walkthrough

For `x = 14`:

```
14 / 5 = 2 remainder 4
```

Moves:

```
5 + 5 + 4
```

Total moves:

```
3
```

## Complexity Analysis

### Time Complexity

O(1)
Only one arithmetic computation is required.

### Space Complexity

O(1)
No additional memory is used.

## Solution Explanation

The solution uses integer division to compute how many full steps of `5` are possible.
If `x` is not exactly divisible by `5`, one additional move covers the remaining distance.

The ternary operator compactly expresses this logic in a single line.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Destination position
    int x;
    cin >> x;

    // Each move can cover at most 5 units
    // If x is divisible by 5, moves = x / 5
    // Otherwise, one extra move is required
    cout << (x % 5 == 0 ? x / 5 : x / 5 + 1);

    return 0;
}
```

## Test Cases Analysis

| x  | x / 5 | Remainder | Output |
| -- | ----- | --------- | ------ |
| 1  | 0     | 1         | 1      |
| 5  | 1     | 0         | 1      |
| 6  | 1     | 1         | 2      |
| 10 | 2     | 0         | 2      |
| 14 | 2     | 4         | 3      |

## Edge Cases to Consider

* `x` less than `5`
* `x` exactly divisible by `5`
* Large values of `x`

## Common Test Cases

* Small values (`1–4`)
* Exact multiples of `5`
* Values just above multiples of `5`

## Common Mistakes to Avoid

* Using floating-point division
* Forgetting the extra move for remainders
* Overcomplicating with loops

## Interview Relevance

* Tests greedy decision-making
* Reinforces integer arithmetic
* Common introductory optimization problem

## What This Problem Teaches

* Greedy strategies using mathematical reasoning
* Effective use of integer division
* Writing concise, readable conditional logic

## Key Takeaways

* Always use the largest possible step when minimizing moves
* Integer division with remainder simplifies greedy problems
* Simple math often replaces simulation

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on mathematical simplification and greedy logic, making it ideal for beginners and interview warm-up practice.