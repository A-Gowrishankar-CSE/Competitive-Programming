# A_Yes_or_Yes

## Platform

Codeforces

## Problem Link

[A. Yes-Yes?](https://codeforces.com/problemset/problem/1759/A)

## Problem Statement

You are given several strings.
For each string, determine whether it represents the word **"YES"**, regardless of letter case.

That is, the string should be considered valid if it matches `"YES"` after converting all characters to uppercase.

## Input Format

* The first line contains an integer `t` — the number of test cases
* Each test case contains a string `s` of length exactly `3`

## Output Format

For each test case:

* Print `"YES"` if the string equals `"YES"` ignoring case
* Print `"NO"` otherwise

## Constraints

* `1 ≤ t ≤ 1000`
* `|s| = 3`
* Each character of `s` is an English letter

## Examples

### Example 1

Input

```
4
YES
yEs
YeS
noo
```

Output

```
YES
YES
YES
NO
```

---

### Example 2

Input

```
3
yes
YeS
abc
```

Output

```
YES
YES
NO
```

## Approach

**Manual case normalization using ASCII values**

## Intuition

The problem requires a **case-insensitive comparison** with the word `"YES"`.

Since the string length is always exactly `3`, each character can be individually converted to uppercase using ASCII manipulation:

* Lowercase letters (`'a'` to `'z'`) have ASCII values greater than `90`
* Subtracting `32` converts a lowercase letter to uppercase

After normalization, a simple string comparison determines the answer.

## Algorithm Steps

* Read the number of test cases `t`
* For each test case:

  * Read string `s`
  * Convert each of the three characters to uppercase if needed
  * Compare the resulting string with `"YES"`
  * Print `"YES"` if they match, otherwise print `"NO"`

## Visual Walkthrough

### Case 1

Input

```
yEs
```

Conversion

```
y → Y
E → E
s → S
```

Resulting string

```
YES
```

Output

```
YES
```

---

### Case 2

Input

```
Noo
```

Conversion

```
N → N
o → O
o → O
```

Resulting string

```
NOO
```

Output

```
NO
```

## Complexity Analysis

### Time Complexity

**O(1)** per test case
Only three characters are processed.

### Space Complexity

**O(1)**
No extra data structures are used.

## Solution Explanation

The solution performs explicit ASCII-based case normalization on each character of the string.

Because the string length is fixed, this approach is straightforward and efficient.

After conversion, a direct comparison with the string `"YES"` yields the correct result.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    int t;
    cin >> t;

    while (t--) {

        string s;
        cin >> s;

        // Convert each character to uppercase if needed
        if (s[0] > 90) s[0] -= 32;
        if (s[1] > 90) s[1] -= 32;
        if (s[2] > 90) s[2] -= 32;

        // Check against "YES"
        if (s == "YES")
            cout << "YES\n";
        else
            cout << "NO\n";
    }

    return 0;
}
```

## Test Cases Analysis

| Input | Normalized | Output |
| ----- | ---------- | ------ |
| YES   | YES        | YES    |
| yEs   | YES        | YES    |
| YeS   | YES        | YES    |
| noo   | NOO        | NO     |
| abc   | ABC        | NO     |

## Edge Cases to Consider

* All lowercase input
* All uppercase input
* Mixed-case input
* Completely unrelated strings

## Common Mistakes to Avoid

* Forgetting case normalization
* Assuming input is always uppercase
* Comparing without converting case

## Interview Relevance

* Tests string handling
* Evaluates understanding of ASCII values
* Common case-insensitive comparison task

## What This Problem Teaches

* Manual character case conversion
* Fixed-length string processing
* Simple validation logic

## Key Takeaways

* ASCII arithmetic can replace library functions
* Fixed constraints simplify implementation
* Case-insensitive checks often require normalization

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on basic string manipulation and character encoding concepts, making it suitable for beginners and early competitive programming practice.