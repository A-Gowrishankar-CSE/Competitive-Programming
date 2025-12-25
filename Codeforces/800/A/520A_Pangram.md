# A_Pangram

## Platform

Codeforces

## Problem Link

[A. Pangram](https://codeforces.com/problemset/problem/520/A)

## Problem Statement

A word or sentence is called a **pangram** if it contains **every letter of the English alphabet at least once**, regardless of case.

You are given a string of length `n` consisting of uppercase and lowercase English letters.
Your task is to determine whether the given string is a pangram.

## Input Format

* The first line contains an integer `n` — the length of the string
* The second line contains a string `s` of length `n`

## Output Format

* Print `"YES"` if the string is a pangram
* Print `"NO"` otherwise

## Constraints

* `1 ≤ n ≤ 100`
* The string contains only English letters (`A–Z`, `a–z`)

## Examples

### Example 1

Input

```
26
abcdefghijklmnopqrstuvwxyz
```

Explanation

All 26 English letters are present.

Output

```
YES
```

---

### Example 2

Input

```
35
TheQuickBrownFoxJumpsOverTheLazyDog
```

Explanation

All letters from `a` to `z` appear at least once, ignoring case.

Output

```
YES
```

---

### Example 3

Input

```
10
Codeforces
```

Explanation

Not all letters of the English alphabet are present.

Output

```
NO
```

## Approach

**Character presence tracking using a boolean array**

## Intuition

A pangram must include **all 26 letters** of the English alphabet.

If the string length is less than 26, it is impossible for it to be a pangram.
Otherwise, each character can be mapped to an index from `0` to `25` and marked as present.

After processing the string, if any letter is missing, the string is not a pangram.

## Algorithm Steps

* Read the integer `n`
* If `n` is less than `26`, print `"NO"` and terminate
* Initialize a boolean array of size `26` to track letter presence
* Read the string `s`
* For each character in the string:

  * Convert it to a zero-based alphabet index
  * Mark the corresponding position as `true`
* Check the boolean array:

  * If any position is `false`, print `"NO"`
  * Otherwise, print `"YES"`

## Visual Walkthrough

### Case 1

Input

```
n = 26
s = abcdefghijklmnopqrstuvwxyz
```

Tracking

```
a → index 0 → marked
b → index 1 → marked
...
z → index 25 → marked
```

All positions are `true`.

Result

```
YES
```

---

### Case 2

Input

```
n = 11
s = HelloWorld
```

Tracking

```
Missing letters: a, b, c, f, g, ...
```

Result

```
NO
```

---

### Case 3

Input

```
n = 28
s = AbCdEfGhIjKlMnOpQrStUvWxYz
```

Tracking

Uppercase and lowercase letters are both mapped correctly.

Result

```
YES
```

## Complexity Analysis

### Time Complexity

**O(n)**

Each character of the string is processed exactly once.

### Space Complexity

**O(1)**

A fixed-size boolean array of 26 elements is used, independent of input size.

## Solution Explanation

The solution efficiently determines pangram validity by:

* Eliminating impossible cases early using the length check
* Tracking letter occurrences using a boolean array
* Handling both uppercase and lowercase letters through ASCII-based indexing

This ensures correctness while keeping the implementation simple and performant.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Length of the string
    int n;
    cin >> n;

    // If length is less than 26, it cannot be a pangram
    if (n < 26) {
        cout << "NO\n";
        return 0;
    }

    // Boolean array to track presence of each letter
    bool f[26] = { false };

    // Input string
    string s;
    cin >> s;

    // Mark the presence of each character
    for (char ch : s) {

        // If character is lowercase
        if (ch > 92) {
            f[ch - 'a'] = true;
        }
        // If character is uppercase
        else {
            f[ch - 'A'] = true;
        }
    }

    // Check if all letters are present
    for (bool present : f) {
        if (!present) {
            cout << "NO\n";
            return 0;
        }
    }

    // All letters are present
    cout << "YES\n";
    return 0;
}
```

## Test Cases Analysis

| Input Length | String Example                      | Output |
| ------------ | ----------------------------------- | ------ |
| 26           | abcdefghijklmnopqrstuvwxyz          | YES    |
| 35           | TheQuickBrownFoxJumpsOverTheLazyDog | YES    |
| 10           | Codeforces                          | NO     |
| 26           | AaBbCcDdEeFfGgHhIiJjKkLlMm          | NO     |

## Edge Cases to Consider

* String length exactly `26`
* All characters in uppercase
* All characters in lowercase
* Repeated letters with some missing letters

## Common Test Cases

* Valid pangram with mixed cases
* Non-pangram due to missing letters
* Minimum length input

## Common Mistakes to Avoid

* Ignoring case sensitivity
* Forgetting the early length check
* Incorrect ASCII value handling

## Interview Relevance

* Tests understanding of character encoding
* Evaluates use of fixed-size frequency arrays
* Common string-processing interview problem

## What This Problem Teaches

* Efficient character presence tracking
* Case-insensitive string handling
* Early termination for optimization

## Key Takeaways

* Pangram checks require exactly 26 unique letters
* Fixed-size arrays are ideal for alphabet-based problems
* ASCII-based indexing simplifies character mapping

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It emphasizes basic string processing and logical checks, making it suitable for beginners and foundational interview preparation.