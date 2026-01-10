# A_Creating_Words

## Platform

Codeforces

## Problem Link

[A. Creating Words](https://codeforces.com/problemset/problem/1985/A)

## Problem Statement

You are given multiple test cases.
In each test case, two strings are provided.

Your task is to create **two new words** by **swapping the first characters** of the given strings.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each of the next `t` lines contains two strings `a` and `b`.

## Output Format

For each test case, print the two modified strings after swapping their first characters.

The two strings should be printed on the same line, separated by a space.

## Constraints

* `1 ≤ t ≤ 1000`
* Each string contains only lowercase English letters
* Length of each string is at least `1`

## Examples

### Example 1

Input

```
3
code forces
hello world
a b
```

Explanation

* Test case 1:

  * Swap `c` and `f`
  * Result → `fode corces`
* Test case 2:

  * Swap `h` and `w`
  * Result → `wello horld`
* Test case 3:

  * Swap `a` and `b`
  * Result → `b a`

Output

```
fode corces
wello horld
b a
```

### Example 2

Input

```
1
program contest
```

Explanation

* Swap `p` and `c`
* Result → `crogram pontest`

Output

```
crogram pontest
```

## Approach (Algorithm Name / Type)

**Character Swap Using Temporary Storage**

This approach swaps the first characters of two strings using a temporary variable.

## Intuition

Each string has at least one character.
By exchanging their first characters:

* The remainder of each string stays unchanged
* Only the leading character is modified

This results in two new valid words without any complex string manipulation.

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read strings `a` and `b`
  * Store `a[0]` in a temporary variable
  * Assign `b[0]` to `a[0]`
  * Assign the temporary variable to `b[0]`
  * Print the updated strings

## Visual Walkthrough

### Test Case 1

Input:

```
a = "code"
b = "forces"
```

Swap process:

```
temp = 'c'
a[0] = 'f'
b[0] = 'c'
```

Result:

```
a = "fode"
b = "corces"
```

---

### Test Case 2

Input:

```
a = "hello"
b = "world"
```

Result:

```
a = "wello"
b = "horld"
```

---

### Test Case 3

Input:

```
a = "a"
b = "b"
```

Result:

```
a = "b"
b = "a"
```

## Complexity Analysis

### Time Complexity

**O(1)** per test case

Only constant-time operations are performed on the first characters.

### Space Complexity

**O(1)**

No additional memory is used beyond a single temporary variable.

## Solution Explanation

The solution performs a direct character swap on the first positions of both strings.

Because strings are mutable and indexing is constant time, this operation is efficient and safe under the given constraints.

The approach ensures clarity, simplicity, and correctness.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while (t--) {

        // Read the two input strings
        string a, b;
        cin >> a >> b;

        // Store the first character of 'a'
        char temp = a[0];

        // Swap the first characters
        a[0] = b[0];
        b[0] = temp;

        // Output the modified strings
        cout << a << " " << b << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Input Strings     | Output Strings    |
| ----------------- | ----------------- |
| `code forces`     | `fode corces`     |
| `hello world`     | `wello horld`     |
| `a b`             | `b a`             |
| `program contest` | `crogram pontest` |

## Edge Cases to Consider

* Strings of length `1`
* Identical first characters
* Very short strings

## Common Test Cases

* Words of equal length
* Words of different lengths
* Single-character strings

## Common Mistakes to Avoid

* Forgetting to store the first character before overwriting
* Attempting to swap entire strings instead of characters
* Incorrect output formatting

## Interview Relevance

* Tests basic string manipulation
* Evaluates understanding of indexing
* Common warm-up problem in interviews

## What This Problem Teaches

* Safe character swapping techniques
* Direct manipulation of string data
* Importance of temporary storage in swaps

## Key Takeaways

* Simple string operations can solve many problems
* Always preserve original data before overwriting
* Clean and minimal logic improves readability

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on fundamental string manipulation and is ideal for beginners and quick interview exercises.