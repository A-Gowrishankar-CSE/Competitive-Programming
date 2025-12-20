# A. Soldier and Bananas

## Platform

Codeforces

## Problem Link

[A. Soldier and Bananas](https://codeforces.com/problemset/problem/546/A)

## Problem Statement

A soldier wants to buy `w` bananas.

* The cost of the **first banana** is `k`
* Each next banana costs `k` more than the previous one

So the prices are:

```
k, 2k, 3k, ..., wk
```

The soldier initially has `n` dollars.

Determine how much money the soldier needs to **borrow** from his friend to buy all `w` bananas.
If he already has enough money, print `0`.

## Input Format

* A single line containing three integers `k`, `n`, and `w`

## Output Format

* Print a single integer representing the amount of money to borrow

## Constraints

* `1 ≤ k, n, w ≤ 1000`

## Examples

### Example 1

Input

```
3 17 4
```

Explanation
Cost of bananas:

```
3 + 6 + 9 + 12 = 30
```

Money the soldier has:

```
17
```

Borrowed amount:

```
30 - 17 = 13
```

Output

```
13
```

---

### Example 2

Input

```
3 100 4
```

Explanation
Total cost:

```
30
```

Since the soldier already has enough money, no borrowing is needed.

Output

```
0
```

---

## Approach

Mathematical summation using arithmetic series.

## Intuition

* The banana prices form an arithmetic sequence.
* The total cost is the sum of the first `w` natural numbers multiplied by `k`.
* If the total cost exceeds the money the soldier has, the difference is the borrowed amount.

## Algorithm Steps

* Read values `k`, `n`, and `w`
* Compute the total cost using the formula:

  ```
  k × (1 + 2 + ... + w)
  ```
* Subtract `n` from the total cost
* If the result is negative, output `0`
* Otherwise, output the result

## Visual Walkthrough

For `k = 2`, `w = 5`:

```
Prices: 2, 4, 6, 8, 10
Sum:    30
```

If `n = 18`:

```
Borrow = 30 - 18 = 12
```

## Complexity Analysis

### Time Complexity

O(1)
Only constant-time arithmetic operations are used.

### Space Complexity

O(1)
No additional memory is required.

## Solution Explanation

The solution uses the arithmetic series formula:

```
1 + 2 + ... + w = w × (w + 1) / 2
```

Multiplying this sum by `k` gives the total cost of all bananas.
Subtracting the soldier’s initial money `n` yields the borrowed amount.
If the result is negative, the soldier does not need to borrow any money.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // k = cost of first banana
    // n = money the soldier has
    // w = number of bananas to buy
    int k, n, w;
    cin >> k >> n >> w;

    // Total cost is:
    // k * (1 + 2 + ... + w)
    // Sum of first w natural numbers = w * (w + 1) / 2
    int borrow = k * w * (w + 1) / 2 - n;

    // If borrow is negative, soldier does not need to borrow money
    cout << (borrow < 0 ? 0 : borrow) << endl;

    return 0;
}
```

## Test Cases Analysis

| k | n   | w | Total Cost | Borrow |
| - | --- | - | ---------- | ------ |
| 3 | 17  | 4 | 30         | 13     |
| 3 | 100 | 4 | 30         | 0      |
| 1 | 0   | 1 | 1          | 1      |
| 5 | 20  | 2 | 15         | 0      |

## Edge Cases to Consider

* Soldier already has sufficient money
* Buying only one banana
* Very small or very large values of `k`, `n`, or `w`

## Common Test Cases

* Exact money match
* Insufficient money
* Minimal input values

## Common Mistakes to Avoid

* Forgetting to apply the arithmetic series formula
* Using loops instead of constant-time math
* Printing negative borrow values

## Interview Relevance

* Tests arithmetic series knowledge
* Demonstrates mathematical optimization
* Common introductory problem in interviews

## What This Problem Teaches

* Applying mathematical formulas to reduce complexity
* Avoiding unnecessary iteration
* Clean handling of conditional outputs

## Key Takeaways

* Arithmetic progressions simplify cost calculations
* Always handle negative results explicitly
* Constant-time solutions are preferred when possible

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on mathematical reasoning and efficient computation, making it ideal for beginners and competitive programming practice.