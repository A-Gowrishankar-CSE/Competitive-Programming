# A. Helpful Maths

## Platform

Codeforces

## Problem Link

[A. Helpful Maths](https://codeforces.com/problemset/problem/339/A)

## Problem Statement

You are given a string consisting of single-digit numbers (`1`, `2`, `3`) separated by `'+'` symbols.

Your task is to **rearrange the numbers** so that they appear in **non-decreasing order**, while keeping the `'+'` symbols between them.

## Input Format

* A single string `s` representing the sum expression.

## Output Format

* Print the rearranged expression in non-decreasing numerical order.

## Constraints

* `1 ≤ length(s) ≤ 100`
* Each number is a single digit (`1`, `2`, or `3`)
* The expression is always valid and well-formed

## Examples

### Example 1

Input

```
3+2+1
```

Explanation
Extracted numbers:

```
3, 2, 1
```

After sorting:

```
1, 2, 3
```

Output

```
1+2+3
```

---

### Example 2

Input

```
1+1+3+1+3
```

Explanation
Sorted numbers:

```
1, 1, 1, 3, 3
```

Output

```
1+1+1+3+3
```

---

## Approach

Parsing and sorting.

## Intuition

* The `'+'` characters are only separators and do not affect numeric ordering.
* By extracting all digits, sorting them, and then reconstructing the expression, the problem becomes straightforward.
* Since all numbers are single-digit, simple integer sorting suffices.

## Algorithm Steps

* Read the input string
* Count how many numbers are present
* Extract digits while skipping `'+'`
* Store digits in an array
* Sort the array
* Print the numbers joined by `'+'`

## Visual Walkthrough

Input:

```
2+3+1
```

Extraction:

```
[2, 3, 1]
```

Sorting:

```
[1, 2, 3]
```

Reconstruction:

```
1+2+3
```

## Complexity Analysis

### Time Complexity

O(n log n)
Sorting dominates the runtime.

### Space Complexity

O(n)
An array is used to store extracted numbers.

## Solution Explanation

The solution computes how many numeric values exist by using the length of the string.
Each digit is extracted by ignoring `'+'` characters and converting the remaining characters into integers.

After sorting the digits, the program prints them in order, placing `'+'` symbols between adjacent numbers to recreate the valid expression.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

int main() {

    // Input string representing the sum expression
    string s;
    cin >> s;

    // Number of digits in the expression
    // For an expression like "1+2+3", length is 5
    // Number of digits = length - number of '+' characters
    int idx = 0;
    int n = s.length() - s.length() / 2;

    // Array to store extracted numbers
    int nums[n];

    // Extract digits and ignore '+' symbols
    for (char ch : s) {
        if (ch != '+') {
            nums[idx++] = ch - '0';
        }
    }

    // Sort the extracted numbers
    sort(nums, nums + n);

    // Print the sorted expression with '+' between numbers
    for (int i = 0; i < n - 1; i++) {
        cout << nums[i] << '+';
    }

    // Print the last number without a trailing '+'
    cout << nums[n - 1];

    return 0;
}
```

## Test Cases Analysis

| Input     | Extracted Digits | Sorted Order | Output    |
| --------- | ---------------- | ------------ | --------- |
| `3+2+1`   | 3, 2, 1          | 1, 2, 3      | `1+2+3`   |
| `1+1+1`   | 1, 1, 1          | 1, 1, 1      | `1+1+1`   |
| `2+3+3+1` | 2, 3, 3, 1       | 1, 2, 3, 3   | `1+2+3+3` |

## Edge Cases to Consider

* Single number with no `'+'`
* All numbers already sorted
* Maximum-length input string

## Common Test Cases

* Reverse-ordered digits
* Repeated digits
* Mixed order digits

## Common Mistakes to Avoid

* Treating `'+'` as a numeric character
* Printing an extra `'+'` at the end
* Forgetting to convert character digits to integers

## Interview Relevance

* Tests string parsing skills
* Demonstrates sorting and reconstruction
* Common beginner problem in competitive programming

## What This Problem Teaches

* Separating data from delimiters
* Efficient use of standard library sorting
* Clean reconstruction of formatted output

## Key Takeaways

* Parsing simplifies complex-looking strings
* Sorting small datasets is efficient and reliable
* Output formatting matters as much as logic

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It emphasizes basic string manipulation and sorting, making it suitable for beginners and interview warm-up practice.