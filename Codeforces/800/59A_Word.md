# A. Word

## Platform

Codeforces

## Problem Link

[A. Word](https://codeforces.com/problemset/problem/59/A)

## Problem Statement

You are given a word consisting of uppercase and lowercase English letters.

If the number of **lowercase letters** in the word is **greater than or equal to** the number of uppercase letters, convert the entire word to **lowercase**.

Otherwise, convert the entire word to **uppercase**.

## Input Format

* A single string `s` representing the word.

## Output Format

* Print the modified word after applying the required case conversion.

## Constraints

* `1 ≤ length(s) ≤ 100`
* The string contains only English alphabet letters

## Examples

### Example 1

Input

```
HoUse
```

Explanation
Lowercase letters: `o, u, s, e` → 4
Uppercase letters: `H` → 1

Since lowercase ≥ uppercase, convert the entire word to lowercase.

Output

```
house
```

---

### Example 2

Input

```
ViP
```

Explanation
Lowercase letters: `i` → 1
Uppercase letters: `V, P` → 2

Since uppercase > lowercase, convert the entire word to uppercase.

Output

```
VIP
```

---

## Approach

Character counting with conditional case conversion.

## Intuition

* The decision depends on which case appears more frequently.
* ASCII values allow quick detection and conversion between lowercase and uppercase.
* Once the dominant case is known, the entire string is converted accordingly.

## Algorithm Steps

* Read the input string
* Count how many lowercase letters are present
* Compare lowercase count with uppercase count
* Convert the entire string to the dominant case
* Output the modified string

## Visual Walkthrough

Input:

```
cODe
```

Counts:

```
Lowercase: c, e → 2
Uppercase: O, D → 2
```

Since lowercase ≥ uppercase:

```
code
```

## Complexity Analysis

### Time Complexity

O(n)
Each character is processed a constant number of times.

### Space Complexity

O(1)
Only counters and in-place string modification are used.

## Solution Explanation

The program first counts the number of lowercase characters by checking ASCII values.
If the lowercase count is greater than or equal to the uppercase count, the string is converted entirely to lowercase.
Otherwise, it is converted entirely to uppercase.

All conversions are done directly using ASCII arithmetic, ensuring efficiency.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Input word
    string s;
    cin >> s;

    // Length of the string
    int n = s.length();

    // Count of lowercase characters
    int lowerCount = 0;

    // Count lowercase letters using ASCII values
    for (char ch : s) {
        if (ch > 92) {
            lowerCount++;
        }
    }

    // If lowercase letters are more or equal,
    // convert entire string to lowercase
    if (lowerCount >= n - lowerCount) {

        for (int i = 0; i < n; i++) {
            // Convert uppercase to lowercase
            if (s[i] <= 92) {
                s[i] += 32;
            }
        }

    } else {
        // Otherwise, convert entire string to uppercase
        for (int i = 0; i < n; i++) {
            // Convert lowercase to uppercase
            if (s[i] > 92) {
                s[i] -= 32;
            }
        }
    }

    // Output the final result
    cout << s << endl;

    return 0;
}
```

## Test Cases Analysis

| Input   | Lowercase | Uppercase | Output |
| ------- | --------- | --------- | ------ |
| `HoUse` | 4         | 1         | house  |
| `ViP`   | 1         | 2         | VIP    |
| `cODe`  | 2         | 2         | code   |
| `ABC`   | 0         | 3         | ABC    |

## Edge Cases to Consider

* All characters already lowercase
* All characters already uppercase
* Equal number of lowercase and uppercase letters

## Common Test Cases

* Mixed-case words
* Single-character strings
* Balanced case counts

## Common Mistakes to Avoid

* Comparing incorrect ASCII ranges
* Converting characters unnecessarily
* Forgetting in-place modification

## Interview Relevance

* Tests string manipulation skills
* Reinforces ASCII value understanding
* Common beginner-level interview problem

## What This Problem Teaches

* Case normalization techniques
* Decision-making based on character statistics
* Efficient in-place string updates

## Key Takeaways

* Dominant-case logic simplifies decision making
* ASCII arithmetic enables fast conversions
* Always handle tie conditions explicitly

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on basic string processing and conditional logic, making it ideal for beginners and competitive programming practice.