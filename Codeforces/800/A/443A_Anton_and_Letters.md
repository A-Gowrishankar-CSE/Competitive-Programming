# A_Anton_and_Letters

## Platform

Codeforces

## Problem Link

[A. Anton and Letters](https://codeforces.com/problemset/problem/443/A)

## Problem Statement

Anton has a set of lowercase English letters written inside curly braces `{}` and separated by commas.

Your task is to determine **how many distinct lowercase letters** are present in the set.

Only lowercase English letters (`a` to `z`) should be considered.
All other characters such as braces, commas, and spaces must be ignored.

## Input Format

* A single line containing a string `s`
  The string represents a set of letters enclosed in `{}`

## Output Format

* Print a single integer — the number of **distinct lowercase letters**

## Constraints

* `1 ≤ |s| ≤ 1000`
* The string may contain:

  * Lowercase letters
  * `{`, `}`, `,`, and spaces

## Examples

### Example 1

Input

```
{a, b, c}
```

Explanation

Distinct letters:

```
a, b, c
```

Count = `3`

Output

```
3
```

---

### Example 2

Input

```
{a, a, b, c}
```

Explanation

Distinct letters:

```
a, b, c
```

Count = `3`

Output

```
3
```

---

### Example 3

Input

```
{}
```

Explanation

No letters are present.

Output

```
0
```

## Approach

**Character filtering and frequency tracking using a boolean array**

## Intuition

The input contains many non-letter characters that are irrelevant.

By scanning the string character by character and marking the presence of each lowercase letter, we can easily count how many **unique letters** appear.

Since there are only 26 lowercase English letters, a fixed-size boolean array is sufficient and efficient.

## Algorithm Steps

* Read the entire input line as a string
* Initialize a boolean array of size `26` to track letter presence
* Traverse each character in the string:

  * If it is a lowercase letter (`a` to `z`), mark it as present
* Count how many positions in the boolean array are marked
* Output the count

## Visual Walkthrough

### Case 1

Input

```
{a, b, c}
```

Processing

```
a → marked
b → marked
c → marked
```

Boolean array status

```
[a, b, c] → true
others    → false
```

Result

```
3
```

---

### Case 2

Input

```
{a, a, a}
```

Processing

```
a → marked once
```

Boolean array status

```
[a] → true
```

Result

```
1
```

---

### Case 3

Input

```
{}
```

Processing

```
No lowercase letters found
```

Result

```
0
```

## Complexity Analysis

### Time Complexity

**O(n)**

Each character of the input string is examined once.

### Space Complexity

**O(1)**

A fixed-size boolean array of 26 elements is used.

## Solution Explanation

The solution ignores all non-letter characters and focuses only on lowercase English letters.

By marking each letter’s presence in a boolean array and counting the marked entries, the program efficiently determines the number of distinct letters.

This method avoids duplicates naturally and aligns directly with the problem requirements.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Read the entire input line
    string s;
    getline(cin, s);

    // Boolean array to track presence of each lowercase letter
    bool f[26] = { 0 };

    // Traverse each character in the string
    for (char ch : s) {

        // Check if the character is a lowercase letter
        if (ch >= 97 && ch <= 122) {
            f[ch - 'a'] = 1;
        }
    }

    // Count distinct letters
    int count = 0;
    for (bool present : f) {
        if (present) count++;
    }

    // Output the result
    cout << count << endl;

    return 0;
}
```

## Test Cases Analysis

| Input String      | Distinct Letters | Output |
| ----------------- | ---------------- | ------ |
| `{a, b, c}`       | a, b, c          | 3      |
| `{a, a, a}`       | a                | 1      |
| `{}`              | none             | 0      |
| `{x, y, z, x, y}` | x, y, z          | 3      |

## Edge Cases to Consider

* Empty set `{}`
* Repeated letters only
* Single letter in the set
* Long input string with many separators

## Common Test Cases

* Mixed repeated and unique letters
* All 26 letters present
* No valid letters present

## Common Mistakes to Avoid

* Counting duplicate letters multiple times
* Treating commas or spaces as valid characters
* Using unnecessary data structures like maps or sets

## Interview Relevance

* Tests string parsing skills
* Evaluates use of frequency arrays
* Common introductory problem on uniqueness detection

## What This Problem Teaches

* Efficient character filtering
* Use of fixed-size arrays for alphabet problems
* Importance of ignoring irrelevant input characters

## Key Takeaways

* Boolean arrays are ideal for uniqueness checks over small domains
* Always filter input data before processing
* Simpler logic often leads to cleaner solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on basic string processing and uniqueness tracking, making it suitable for beginners and early-stage interview preparation.