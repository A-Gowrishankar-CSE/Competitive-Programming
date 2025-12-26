# A_Insomnia_cure

## Platform

Codeforces

## Problem Link

[A. Insomnia cure](https://codeforces.com/problemset/problem/148/A)

## Problem Statement

A dragon is suffering from insomnia and spends its nights damaging the city.

There are `d` dragons, numbered from `1` to `d`.

The dragon will harm:

* Every `k`-th dragon by hitting it with a frying pan
* Every `l`-th dragon by hitting it with a tail
* Every `m`-th dragon by stepping on it
* Every `n`-th dragon by shouting at it

A dragon is considered **harmed** if **at least one** of the above actions affects it.

Your task is to determine how many dragons are harmed.

## Input Format

* A single line containing five integers
  `k l m n d`

## Output Format

* Print a single integer — the number of harmed dragons

## Constraints

* `1 ≤ k, l, m, n ≤ d ≤ 10^5`

## Examples

### Example 1

Input

```
1 2 3 4 12
```

Explanation

Since `k = 1`, every dragon is harmed.

Output

```
12
```

---

### Example 2

Input

```
2 3 4 5 24
```

Explanation

Dragons harmed are those divisible by `2`, `3`, `4`, or `5`.

Output

```
17
```

---

### Example 3

Input

```
3 4 5 6 24
```

Explanation

Only dragons divisible by at least one of the given values are harmed.

Output

```
10
```

## Approach

**Brute-force divisibility checking**

## Intuition

Each dragon is checked independently.

If a dragon number is divisible by **any** of the given values (`k`, `l`, `m`, or `n`), it is harmed.

Since the number of dragons is reasonably small, a simple loop with modulo checks is efficient and clear.

## Algorithm Steps

* Read integers `k`, `l`, `m`, `n`, and `d`
* Initialize a counter to store the number of harmed dragons
* For every dragon number from `1` to `d`:

  * If the number is divisible by any of `k`, `l`, `m`, or `n`, increment the counter
* Print the final count

## Visual Walkthrough

### Case 1

Input

```
k = 2, l = 3, m = 4, n = 5, d = 12
```

Harmed dragons

```
2, 3, 4, 5, 6, 8, 9, 10, 12
```

Total harmed

```
9
```

---

### Case 2

Input

```
k = 1, l = 2, m = 3, n = 4, d = 7
```

Since `k = 1`, every dragon is harmed.

Result

```
7
```

---

### Case 3

Input

```
k = 3, l = 5, m = 7, n = 11, d = 20
```

Harmed dragons

```
3, 5, 6, 7, 9, 10, 11, 12, 14, 15, 18, 20
```

Total harmed

```
12
```

## Complexity Analysis

### Time Complexity

**O(d)**

Each dragon from `1` to `d` is checked exactly once.

### Space Complexity

**O(1)**

Only a few integer variables are used.

## Solution Explanation

The solution iterates through all dragons and checks divisibility against the four given integers.

The logical OR condition ensures that each dragon is counted only once, even if it satisfies multiple divisibility conditions.

This straightforward approach directly matches the problem constraints and is easy to understand and implement.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Read input values
    int k, l, m, n, d;
    cin >> k >> l >> m >> n >> d;

    // Counter for harmed dragons
    int harmed = 0;

    // Check each dragon
    for (int i = 1; i <= d; i++) {

        // If dragon i is harmed by at least one action
        if (i % k == 0 || i % l == 0 || i % m == 0 || i % n == 0) {
            harmed++;
        }
    }

    // Output the result
    cout << harmed << endl;

    return 0;
}
```

## Test Cases Analysis

| k | l  | m  | n  | d  | Output |
| - | -- | -- | -- | -- | ------ |
| 1 | 2  | 3  | 4  | 12 | 12     |
| 2 | 3  | 4  | 5  | 24 | 17     |
| 3 | 4  | 5  | 6  | 24 | 10     |
| 7 | 11 | 13 | 17 | 20 | 2      |

## Edge Cases to Consider

* One of `k`, `l`, `m`, or `n` equals `1`
* All values are greater than `d`
* `d = 1`
* Overlapping divisibility conditions

## Common Test Cases

* Small values of `d`
* Large values of `d`
* Cases with frequent overlaps

## Common Mistakes to Avoid

* Counting a dragon multiple times
* Incorrect loop bounds
* Forgetting to include all four divisibility checks

## Interview Relevance

* Tests understanding of loops and conditional logic
* Evaluates basic number theory concepts
* Common beginner-level problem

## What This Problem Teaches

* Efficient use of conditional checks
* Logical OR conditions
* Translating problem statements into simple loops

## Key Takeaways

* Brute-force solutions are acceptable when constraints are small
* Always check “at least one” conditions carefully
* Simplicity often leads to the clearest solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on basic iteration and divisibility logic, making it ideal for beginners and early competitive programming practice.