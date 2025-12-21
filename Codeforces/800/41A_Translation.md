# A. Translation

## Platform

Codeforces

## Problem Link

[A. Translation](https://codeforces.com/problemset/problem/41/A)

## Problem Statement

You are given two strings.

Determine whether the second string is exactly the **reverse** of the first string.

If it is, print `"YES"`. Otherwise, print `"NO"`.

## Input Format

* The first line contains a string `s1`
* The second line contains a string `s2`

Both strings consist of lowercase English letters.

## Output Format

Print `"YES"` if `s2` is the reverse of `s1`.
Otherwise, print `"NO"`.

## Constraints

* `1 ≤ length of s1, s2 ≤ 100`
* Strings contain only lowercase English letters

## Examples

### Example 1

Input

```
code
edoc
```

Explanation
Reversing `"code"` gives `"edoc"`, which matches the second string.

Output

```
YES
```

### Example 2

Input

```
abc
abd
```

Explanation
Reversing `"abc"` gives `"cba"`, which does not match `"abd"`.

Output

```
NO
```

### Example 3

Input

```
a
a
```

Explanation
Single-character strings remain the same when reversed.

Output

```
YES
```

## Approach

Two different string-handling approaches are used:

* Manual reverse comparison using index traversal
* Built-in string reversal using the Standard Template Library (STL)

## Intuition

The problem directly checks a **string reversal condition**.

If the second string is formed by reversing the first string character by character, the answer is `"YES"`.
Otherwise, it is `"NO"`.

Both approaches validate this rule using different techniques.

## Algorithm Steps

**Approach 1: Manual Character Comparison**

* Read both strings
* If their lengths differ, print `"NO"`
* Traverse the first string from left to right
* Compare each character with the corresponding character from the end of the second string
* If any mismatch occurs, print `"NO"`
* If all characters match, print `"YES"`

**Approach 2: STL Reverse Function**

* Read both strings
* Reverse the second string using `reverse()`
* Compare the two strings directly
* Print `"YES"` if equal, otherwise `"NO"`

## Visual Walkthrough

For input:

```
s1 = "abcd"
s2 = "dcba"
```

Character comparison:

```
s1[0] == s2[3]  → a == a
s1[1] == s2[2]  → b == b
s1[2] == s2[1]  → c == c
s1[3] == s2[0]  → d == d
```

All characters match → `"YES"`

## Complexity Analysis

### Time Complexity

* Approach 1: **O(n)**
* Approach 2: **O(n)**

Where `n` is the length of the string.

### Space Complexity

* Approach 1: **O(1)** (no extra data structures)
* Approach 2: **O(1)** (in-place reversal)

## Solution Explanation

The solution verifies whether the second string is the exact reverse of the first.

The first approach performs a manual character-by-character comparison, giving complete control over the logic and avoiding extra operations.

The second approach uses the STL `reverse()` function, making the solution concise and readable.

Both methods are efficient and fully satisfy the problem requirements.

## Full Solution

### Approach 1: Manual Reverse Comparison (C++)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Declare two strings
    string s1, s2;

    // Read input strings
    cin >> s1 >> s2;

    // If lengths are not equal, they cannot be reverses
    if (s1.length() != s2.length()) {
        cout << "NO\n";
        return 0;
    }

    // Store length of the string
    int n = s1.length();

    // Compare characters from start of s1 and end of s2
    for (int i = 0; i < n; i++) {

        // If any character does not match, print NO
        if (s1[i] != s2[n - i - 1]) {
            cout << "NO\n";
            return 0;
        }
    }

    // If all characters match, print YES
    cout << "YES\n";

    return 0;
}
```

### Approach 2: Using STL Reverse Function (C++)

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

int main() {

    // Declare two strings
    string s1, s2;

    // Read input strings
    cin >> s1 >> s2;

    // Reverse the second string using STL
    reverse(s2.begin(), s2.end());

    // Compare both strings and print result
    cout << (s1 == s2 ? "YES\n" : "NO\n");

    return 0;
}
```

## Test Cases Analysis

| Input     | Expected Output | Reason                  |
| --------- | --------------- | ----------------------- |
| code edoc | YES             | Exact reverse           |
| abc cba   | YES             | Correct reverse         |
| abc abd   | NO              | Characters do not match |
| a a       | YES             | Single-character string |
| ab ba     | YES             | Valid reverse           |

## Edge Cases to Consider

* Single-character strings
* Strings of different lengths
* Strings with repeated characters

## Common Test Cases

* Fully reversed strings
* Non-reversed but similar strings
* Minimum-length strings

## Common Mistakes to Avoid

* Forgetting to check string length first
* Incorrect index calculation (`n - i - 1`)
* Comparing strings without reversing correctly

## Interview Relevance

* Tests understanding of string manipulation
* Evaluates indexing and boundary handling
* Common warm-up problem in technical interviews

## What This Problem Teaches

* Multiple ways to solve the same problem
* Importance of string indexing
* Efficient use of STL functions

## Key Takeaways

* Always verify input constraints first
* STL functions can simplify code significantly
* Manual approaches help build strong fundamentals

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on basic string operations and logical thinking, making it ideal for beginners and interview preparation.
