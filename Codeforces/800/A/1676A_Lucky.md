# A. Lucky

## Platform

Codeforces

## Problem Link

[A. Lucky](https://codeforces.com/problemset/problem/1676/A)

## Problem Statement

You are given several tickets.
Each ticket is represented as a **6-digit string**.

A ticket is considered **lucky** if the **sum of the first three digits** is equal to the **sum of the last three digits**.

For each ticket, determine whether it is lucky.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each of the next `t` lines contains a string `s` of length `6`, consisting only of digits.

## Output Format

For each test case, print:

* `"YES"` if the ticket is lucky
* `"NO"` otherwise

## Constraints

* `1 ≤ t ≤ 1000`
* `s.length = 6`
* `s[i]` is a digit (`0`–`9`)

## Examples

### Example 1

Input

```
3
123321
555555
123456
```

Explanation

* `123321` → `1 + 2 + 3 = 6`, `3 + 2 + 1 = 6` → lucky
* `555555` → `5 + 5 + 5 = 15`, `5 + 5 + 5 = 15` → lucky
* `123456` → `1 + 2 + 3 = 6`, `4 + 5 + 6 = 15` → not lucky

Output

```
YES
YES
NO
```

### Example 2

Input

```
1
000000
```

Explanation
Both halves sum to zero.

Output

```
YES
```

## Approach

**Direct Digit Comparison Using Character Arithmetic**

## Intuition

The ticket length is fixed at 6 digits.
By directly comparing the sum of the first three characters with the sum of the last three characters, we can determine if the ticket is lucky.

Since characters representing digits can be summed directly (their relative values remain consistent), explicit numeric conversion is unnecessary.

## Algorithm Steps

* Read the number of test cases
* For each ticket string:

  * Add the first three characters
  * Add the last three characters
  * Compare the two sums
* Print the result accordingly

## Visual Walkthrough

Ticket:

```
s = "123321"
```

Left half:

```
'1' + '2' + '3'
```

Right half:

```
'3' + '2' + '1'
```

Both sums are equal → lucky ticket.

Another ticket:

```
s = "123456"
```

Left sum ≠ Right sum → not lucky.

## Complexity Analysis

### Time Complexity

O(t)

Each test case processes a constant number of operations.

### Space Complexity

O(1)

Only fixed-size variables are used.

## Solution Explanation

The solution checks whether the sum of the first three characters of the string equals the sum of the last three characters.
Because all characters represent digits and both sides use the same character arithmetic, the comparison is valid and efficient.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each ticket
    while (t--) {

        // Read the 6-digit ticket as a string
        string s;
        cin >> s;

        // Compare sum of first three and last three digits
        if (s[0] + s[1] + s[2] == s[3] + s[4] + s[5]) {
            cout << "YES\n";
        } else {
            cout << "NO\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Ticket | Left Sum | Right Sum | Result |
| ------ | -------- | --------- | ------ |
| 123321 | 6        | 6         | YES    |
| 555555 | 15       | 15        | YES    |
| 123456 | 6        | 15        | NO     |
| 000000 | 0        | 0         | YES    |

## Edge Cases to Consider

* All digits are zero
* All digits are the same
* Minimum and maximum digit values

## Common Test Cases

* Symmetric tickets
* Completely different halves
* Repeated digits

## Common Mistakes to Avoid

* Forgetting to read input as a string
* Using incorrect indices
* Misunderstanding character summation logic

## Interview Relevance

* Tests string indexing
* Evaluates simple arithmetic reasoning
* Common warm-up problem in contests

## What This Problem Teaches

* Working with strings instead of numbers
* Efficient comparison using fixed-size data
* Clean conditional logic

## Key Takeaways

* Fixed-length problems can be solved directly
* Character arithmetic is sufficient for digit comparison
* Simplicity often leads to optimal solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on string manipulation and basic arithmetic, making it ideal for beginners and early interview practice.