# B. Borze

## Platform

Codeforces

## Problem Link

[B. Borze](https://codeforces.com/problemset/problem/32/B)

## Problem Statement

You are given a string consisting only of characters `'.'` and `'-'`.

This string represents a message encoded using the **Borze code**, where:

* `.` corresponds to `0`
* `-.` corresponds to `1`
* `--` corresponds to `2`

Your task is to decode the given string and print the resulting sequence of digits.

## Input Format

* A single string `s` containing only `'.'` and `'-'`

## Output Format

* A decoded string consisting of digits `0`, `1`, and `2`

## Constraints

* `1 ≤ |s| ≤ 200`
* The string is guaranteed to be a valid Borze encoding

## Examples

### Example 1

Input

```
.-.--.
```

Explanation

Decoding step-by-step:

```
.   → 0
-.  → 1
--  → 2
.
```

Output

```
0120
```

### Example 2

Input

```
--..-.
```

Explanation

Decoding:

```
-- → 2
.  → 0
.  → 0
-. → 1
```

Output

```
2001
```

## Approach

**Sequential Parsing with Lookahead**

## Intuition

The encoding rules are prefix-based:

* A single `.` always maps to `0`
* A `-` always begins a two-character sequence

So when a `-` is encountered:

* Look at the next character to determine whether it is `-.` or `--`
* Decode accordingly and skip the next character

This guarantees linear processing of the string.

## Algorithm Steps

* Read the encoded string `s`
* Iterate through the string using an index `i`
* If `s[i]` is `.`:

  * Output `0`
* If `s[i]` is `-`:

  * Check `s[i + 1]`
  * Output `1` if `-.`
  * Output `2` if `--`
  * Increment `i` to skip the processed character
* Continue until the end of the string

## Visual Walkthrough

Input:

```
s = ".-.-"
```

Processing:

```
i = 0 → '.' → 0
i = 1 → '-' and next is '.' → 1
i = 3 → '-' and next is '.' → 1
```

Output:

```
011
```

## Complexity Analysis

### Time Complexity

O(n)

Each character is processed at most once.

### Space Complexity

O(1)

No additional data structures are used.

## Solution Explanation

The solution uses a single pass through the string.
When encountering a dash, it performs a constant-time lookahead to decode the correct digit.

The index is manually incremented to avoid reprocessing characters that belong to a two-character encoding.

This approach is simple, efficient, and aligns perfectly with the problem constraints.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Read the encoded Borze string
    string s;
    cin >> s;

    // Iterate through the string
    for (int i = 0; i < s.length(); i++) {

        // Single dot represents 0
        if (s[i] == '.') {
            cout << '0';
        }

        // Dash always starts a two-character code
        else if (s[i] == '-') {

            // Check the next character to determine the code
            if (s[i + 1] == '.') {
                cout << '1';  // "-."
            } else {
                cout << '2';  // "--"
            }

            // Skip the next character as it has been processed
            i++;
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Input    | Decoded |
| -------- | ------- |
| `.`      | 0       |
| `-.`     | 1       |
| `--`     | 2       |
| `.-.--.` | 0120    |
| `--..-.` | 2001    |

## Edge Cases to Consider

* String containing only dots
* String containing only dashes
* Alternating patterns

## Common Test Cases

* Mixed sequences
* Long valid Borze strings
* Minimal length input

## Common Mistakes to Avoid

* Forgetting to increment the index after processing `-`
* Treating `-` as a standalone character
* Out-of-bounds access without guaranteed valid input

## Interview Relevance

* Tests string parsing skills
* Demonstrates controlled index manipulation
* Common decoding-style problem

## What This Problem Teaches

* Parsing encoded strings
* Using lookahead safely
* Writing clean single-pass logic

## Key Takeaways

* Prefix-based encodings are often decoded sequentially
* Lookahead is powerful when rules are simple
* Always manage indices carefully

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on string traversal and conditional decoding, making it ideal for beginner and intermediate competitive programmers.