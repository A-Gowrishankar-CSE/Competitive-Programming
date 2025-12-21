# A. Wrong Subtraction

## Platform

Codeforces

## Problem Link

[A. Wrong Subtraction](https://codeforces.com/problemset/problem/977/A)

## Problem Statement

You are given two integers `n` and `k`.

You must perform the following operation **exactly `k` times**:

* If the last digit of `n` is **non-zero**, subtract `1` from `n`
* If the last digit of `n` is **zero**, divide `n` by `10`

After performing all `k` operations, output the resulting value of `n`.

## Input Format

* A single line containing two integers `n` and `k`

## Output Format

* Print the final value of `n` after `k` operations

## Constraints

* `1 ≤ n ≤ 10^9`
* `1 ≤ k ≤ 50`

## Examples

### Example 1

Input

```
512 4
```

Explanation
Step-by-step operations:

```
512 → 511 → 510 → 51 → 50
```

Output

```
50
```

---

### Example 2

Input

```
1000 1
```

Explanation
Last digit is zero, so divide by 10:

```
1000 → 100
```

Output

```
100
```

---

## Approach

Iterative simulation.

## Intuition

* The operation rules are straightforward and depend only on the last digit.
* Since `k` is small, simulating each step is efficient and clear.
* The modulo operation (`n % 10`) is ideal for checking the last digit.

## Algorithm Steps

* Read values `n` and `k`
* Repeat the operation `k` times:

  * If `n % 10 != 0`, decrement `n`
  * Else, divide `n` by `10`
* Output the final value of `n`

## Visual Walkthrough

For `n = 200`, `k = 3`:

```
200 → 20 → 2 → 1
```

Operations:

* Step 1: last digit 0 → divide by 10
* Step 2: last digit 0 → divide by 10
* Step 3: last digit 2 → subtract 1

## Complexity Analysis

### Time Complexity

O(k)
Each operation is performed once.

### Space Complexity

O(1)
No additional memory is used.

## Solution Explanation

The program directly follows the problem’s rules.
It checks the last digit of `n` using the modulo operator.
Based on this check, it either subtracts `1` or divides `n` by `10`.

Repeating this process `k` times yields the correct final value.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Initial number and number of operations
    int n, k;
    cin >> n >> k;

    // Perform the operation k times
    while (k--) {

        // If the last digit is non-zero, subtract 1
        if (n % 10) {
            n--;
        }
        // If the last digit is zero, divide by 10
        else {
            n /= 10;
        }
    }

    // Output the final result
    cout << n << endl;

    return 0;
}
```

## Test Cases Analysis

| n    | k | Final Value |
| ---- | - | ----------- |
| 512  | 4 | 50          |
| 1000 | 1 | 100         |
| 10   | 2 | 1           |
| 1    | 1 | 0           |

## Edge Cases to Consider

* `n` ending with multiple zeros
* `k` equal to the number of digits
* Small values of `n`

## Common Test Cases

* Large numbers with trailing zeros
* Single-digit numbers
* Mixed decrement and division operations

## Common Mistakes to Avoid

* Forgetting to update `n` inside the loop
* Using floating-point division
* Misinterpreting the operation order

## Interview Relevance

* Tests conditional logic and loops
* Reinforces number manipulation concepts
* Common introductory simulation problem

## What This Problem Teaches

* Working with digits using modulo operations
* Careful implementation of conditional rules
* Simple simulations can be optimal

## Key Takeaways

* Always follow operation order exactly as specified
* Modulo is effective for digit inspection
* Loop-based simulations are safe when constraints are small

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on basic number manipulation and conditional logic, making it suitable for beginners and competitive programming practice.