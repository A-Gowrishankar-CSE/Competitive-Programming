# A. A+B Again?

## Platform

Codeforces

## Problem Link

[A. A+B Again?](https://codeforces.com/problemset/problem/1772/A)

## Problem Statement

For each test case, you are given a **two-digit integer** `n`.

Your task is to compute the **sum of its digits** and print the result.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case contains a single integer `n`.

```
n
```

## Output Format

For each test case, print a single integer representing the sum of the digits of `n`.

Each answer should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* `10 ≤ n ≤ 99`

## Examples

### Example 1

Input

```
3
12
45
90
```

Explanation

* `12 → 1 + 2 = 3`
* `45 → 4 + 5 = 9`
* `90 → 9 + 0 = 9`

Output

```
3
9
9
```

### Example 2

Input

```
2
10
99
```

Explanation

* `10 → 1 + 0 = 1`
* `99 → 9 + 9 = 18`

Output

```
1
18
```

## Approach

**Digit Extraction Using Arithmetic Operators**

## Intuition

Since `n` is guaranteed to be a two-digit number:

* The **tens digit** is obtained using integer division by 10
* The **units digit** is obtained using modulo 10

Adding these two values gives the required result.

This avoids converting the number into a string and keeps the solution efficient.

## Algorithm Steps

* Read the number of test cases
* For each test case:

  * Read integer `n`
  * Extract the tens digit using `n / 10`
  * Extract the units digit using `n % 10`
  * Print their sum

## Visual Walkthrough

Test case:

```
n = 47
```

Digit extraction:

```
47 / 10 = 4
47 % 10 = 7
```

Sum:

```
4 + 7 = 11
```

Output:

```
11
```

## Complexity Analysis

### Time Complexity

O(t)

Each test case is processed in constant time.

### Space Complexity

O(1)

No extra space is used beyond basic variables.

## Solution Explanation

The solution takes advantage of the mathematical properties of integer division and modulo operations.
By separating the tens and units digits directly, it computes the digit sum efficiently and clearly.

This approach is optimal for the given constraints.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while (t--) {

        // Read the two-digit number
        int n;
        cin >> n;

        // n / 10 extracts the tens digit
        // n % 10 extracts the units digit
        // Their sum gives the required result
        cout << n / 10 + n % 10 << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| n  | Tens Digit | Units Digit | Sum |
| -- | ---------- | ----------- | --- |
| 12 | 1          | 2           | 3   |
| 45 | 4          | 5           | 9   |
| 90 | 9          | 0           | 9   |
| 99 | 9          | 9           | 18  |

## Edge Cases to Consider

* Numbers ending with zero
* Maximum value `99`
* Minimum value `10`

## Common Test Cases

* Small two-digit numbers
* Numbers with identical digits
* Numbers with zero as the second digit

## Common Mistakes to Avoid

* Using string conversion unnecessarily
* Forgetting integer division behavior
* Mishandling multiple test cases

## Interview Relevance

* Tests understanding of digit manipulation
* Reinforces arithmetic operators
* Common beginner-level question

## What This Problem Teaches

* Efficient digit extraction
* Proper use of integer division and modulo
* Clean loop-based input handling

## Key Takeaways

* Arithmetic operations are often faster than string processing
* Always consider constraints before choosing an approach
* Simple problems benefit from simple solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on basic number manipulation and input processing, making it ideal for beginners and competitive programming warm-up exercises.