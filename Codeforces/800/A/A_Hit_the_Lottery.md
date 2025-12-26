# A_Hit_the_Lottery

## Platform

Codeforces

## Problem Link

[A. Hit the Lottery](https://codeforces.com/problemset/problem/996/A)

## Problem Statement

Allen has just won the lottery and received an amount of money represented by an integer `n`.

He wants to withdraw exactly `n` dollars from the bank using the **minimum number of bills**.
The bank provides bills of the following denominations:

```
100, 20, 10, 5, 1
```

Your task is to determine the **minimum number of bills** required to make up the amount `n`.

## Input Format

* A single integer `n` — the amount of money Allen needs to withdraw

## Output Format

* Print a single integer — the minimum number of bills required

## Constraints

* `1 ≤ n ≤ 10^9`
* Unlimited supply of each bill denomination

## Examples

### Example 1

Input

```
125
```

Explanation

```
100 → 1 bill
20  → 1 bill
5   → 1 bill
```

Total bills = `3`

Output

```
3
```

---

### Example 2

Input

```
43
```

Explanation

```
20 → 2 bills
1  → 3 bills
```

Total bills = `5`

Output

```
5
```

---

### Example 3

Input

```
1
```

Explanation

Only one `1`-dollar bill is needed.

Output

```
1
```

## Approach

**Greedy denomination-based subtraction**

## Intuition

To minimize the number of bills, the largest possible denomination should always be used first.

Since the denominations are designed in a way that each smaller bill divides the larger ones logically, a **greedy strategy** guarantees the optimal solution.

The idea is simple:

* Use as many `100`-dollar bills as possible
* Then use `20`, followed by `10`, `5`, and finally `1`

## Algorithm Steps

* Read the integer `n`
* Initialize a counter to store the number of bills used
* While `n` is at least `100`, subtract `100` and increment the counter
* While `n` is at least `20`, subtract `20` and increment the counter
* If `n` is at least `10`, subtract `10` and increment the counter
* If `n` is at least `5`, subtract `5` and increment the counter
* Add the remaining value of `n` (which is less than `5`) directly to the counter
* Output the total count

## Visual Walkthrough

### Case 1

Input

```
n = 289
```

Processing

```
100 → 2 times → remaining 89
20  → 4 times → remaining 9
5   → 1 time  → remaining 4
1   → 4 times
```

Total bills

```
2 + 4 + 1 + 4 = 11
```

---

### Case 2

Input

```
n = 50
```

Processing

```
20 → 2 times → remaining 10
10 → 1 time  → remaining 0
```

Total bills

```
3
```

---

### Case 3

Input

```
n = 7
```

Processing

```
5 → 1 time → remaining 2
1 → 2 times
```

Total bills

```
3
```

## Complexity Analysis

### Time Complexity

**O(n / 100)** in the worst case

Since each loop reduces `n` significantly and the number of iterations is very small, this effectively behaves as **O(1)**.

### Space Complexity

**O(1)**

Only a constant number of variables are used.

## Solution Explanation

The solution repeatedly subtracts the largest possible bill value from the remaining amount.

This greedy approach works because:

* Larger bills always reduce the total count more efficiently
* The denomination system ensures no better combination exists using smaller bills

The final remaining value is less than `5`, so it can be handled directly using `1`-dollar bills.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Amount to withdraw
    int n, bill = 0;
    cin >> n;

    // Use as many 100-dollar bills as possible
    while (n >= 100) {
        bill++;
        n -= 100;
    }

    // Use as many 20-dollar bills as possible
    while (n >= 20) {
        bill++;
        n -= 20;
    }

    // Use one 10-dollar bill if possible
    if (n >= 10) {
        bill++;
        n -= 10;
    }

    // Use one 5-dollar bill if possible
    if (n >= 5) {
        bill++;
        n -= 5;
    }

    // Remaining amount is paid using 1-dollar bills
    bill += n;

    // Output the minimum number of bills
    cout << bill << endl;

    return 0;
}
```

## Test Cases Analysis

| Input `n` | Breakdown                | Output |
| --------- | ------------------------ | ------ |
| 125       | 100 + 20 + 5             | 3      |
| 43        | 20 + 20 + 1 + 1 + 1      | 5      |
| 10        | 10                       | 1      |
| 1         | 1                        | 1      |
| 999       | 100×9 + 20×4 + 10 + 5 +4 | 18     |

## Edge Cases to Consider

* `n = 1`
* `n` exactly equal to a denomination
* Very large values of `n`
* Amounts just below a higher denomination

## Common Test Cases

* Multiples of `100`
* Random mid-range values
* Values requiring all denominations

## Common Mistakes to Avoid

* Using smaller bills before larger ones
* Forgetting to handle the remaining amount less than `5`
* Overcomplicating the solution with unnecessary data structures

## Interview Relevance

* Demonstrates greedy algorithm usage
* Tests understanding of optimal choice strategies
* Commonly asked basic optimization problem

## What This Problem Teaches

* Greedy algorithms can be optimal with the right conditions
* Simple arithmetic can outperform complex logic
* Order of operations matters in optimization problems

## Key Takeaways

* Always try the largest valid option first in minimization problems
* Greedy strategies work well with canonical coin systems
* Clean, readable logic leads to reliable solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on greedy decision-making and arithmetic reasoning, making it suitable for beginners and foundational interview preparation.