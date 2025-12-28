# A_Sum_of_Round_Numbers

## Platform

Codeforces

## Problem Link

[A. Sum of Round Numbers](https://codeforces.com/problemset/problem/1352/A)

## Problem Statement

A **round number** is a number that has exactly **one non-zero digit**, and that digit can appear at any position.

Examples of round numbers:

```
1, 5, 10, 900, 3000
```

Examples of non-round numbers:

```
12, 105, 709
```

You are given an integer `n`.
Your task is to represent `n` as the **sum of round numbers** and output those round numbers.

## Input Format

* The first line contains an integer `t` — the number of test cases
* Each test case contains a single integer `n`

## Output Format

For each test case:

* Print an integer — the count of round numbers
* Print the round numbers themselves on the next line

## Constraints

* `1 ≤ t ≤ 10⁴`
* `1 ≤ n ≤ 10⁹`

## Examples

### Example 1

Input

```
3
5009
7
1000
```

Explanation

```
5009 = 5000 + 9
7    = 7
1000 = 1000
```

Output

```
2
5000 9
1
7
1
1000
```

## Approach

**Digit extraction with positional value tracking**

## Intuition

Each non-zero digit in `n` contributes a **round number** equal to:

```
digit × (10^position)
```

By extracting digits from right to left and multiplying them with the corresponding power of 10, we can directly construct all round numbers whose sum equals `n`.

## Algorithm Steps

* Read the number of test cases `t`
* For each test case:

  * Read integer `n`
  * Initialize `digit = 1` to track powers of 10
  * If the last digit is non-zero, add it directly
  * Remove the last digit
  * For remaining digits:

    * Multiply each digit by `10^digit`
    * If the result is non-zero, store it
    * Increment `digit`
  * Print the count and stored round numbers

## Visual Walkthrough

### Case 1

Input

```
5009
```

Digit processing

```
9    → 9
0    → ignored
0    → ignored
5    → 5000
```

Output

```
2
9 5000
```

---

### Case 2

Input

```
8070
```

Digit processing

```
0    → ignored
7    → 70
0    → ignored
8    → 8000
```

Output

```
2
70 8000
```

---

### Case 3

Input

```
4
```

Digit processing

```
4 → 4
```

Output

```
1
4
```

## Complexity Analysis

### Time Complexity

**O(d)** per test case, where `d` is the number of digits in `n`.

### Space Complexity

**O(d)** to store the round numbers.

## Solution Explanation

The solution decomposes the number digit by digit.

Each digit is multiplied by the appropriate power of 10 to form a round number.
Zero-valued contributions are skipped, ensuring that only valid round numbers are stored.

The sum of all generated round numbers always equals the original number `n`.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
#include <cmath>
#include <vector>
using namespace std;

int main() {

    int t;
    cin >> t;

    while (t--) {

        int n, digit = 1;
        cin >> n;

        vector<int> v;

        // Handle the least significant digit
        if (n % 10)
            v.push_back(n % 10);

        n /= 10;

        // Process remaining digits
        while (n > 0) {

            int ele = (n % 10) * pow(10, digit++);
            if (ele)
                v.push_back(ele);

            n /= 10;
        }

        // Output result
        cout << v.size() << '\n';
        for (int i : v)
            cout << i << " ";
        cout << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Input | Round Numbers | Count |
| ----- | ------------- | ----- |
| 5009  | 5000, 9       | 2     |
| 100   | 100           | 1     |
| 101   | 100, 1        | 2     |
| 7     | 7             | 1     |

## Edge Cases to Consider

* Single-digit numbers
* Numbers with trailing zeros
* Numbers where all digits are non-zero
* Maximum constraint values

## Common Test Cases

* Powers of 10
* Numbers with alternating zero digits
* Large multi-digit numbers

## Common Mistakes to Avoid

* Including zero-valued components
* Incorrect power-of-10 calculation
* Forgetting to reset containers for each test case

## Interview Relevance

* Tests digit manipulation
* Evaluates understanding of place value
* Common decomposition problem in competitive programming

## What This Problem Teaches

* Breaking numbers into positional components
* Efficient digit-based processing
* Translating mathematical observation into code

## Key Takeaways

* Every number can be represented as a sum of round numbers
* Digit-wise processing is often simpler than string conversion
* Filtering zero contributions simplifies output

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on digit extraction and arithmetic decomposition, making it suitable for beginners and foundational problem-solving practice.