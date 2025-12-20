# A. Word Capitalization

## Platform

Codeforces

## Problem Link

[A. Word Capitalization](https://codeforces.com/problemset/problem/281/A)

## Problem Statement

You are given a word consisting of lowercase and/or uppercase English letters.

Your task is to **capitalize the first character** of the word, while keeping all other characters unchanged.

## Input Format

* A single string `s` representing the word.

## Output Format

* Print the resulting word after capitalizing its first character.

## Constraints

* `1 ≤ length(s) ≤ 1000`
* The string contains only English alphabet letters

## Examples

### Example 1

Input

```
word
```

Explanation
The first character `'w'` is converted to `'W'`.

Output

```
Word
```

---

### Example 2

Input

```
Word
```

Explanation
The first character is already uppercase, so the word remains unchanged.

Output

```
Word
```

---

## Approach

Direct ASCII-based character modification.

## Intuition

* In ASCII, lowercase letters have values greater than uppercase letters.
* The difference between lowercase and uppercase characters is `32`.
* By checking whether the first character is lowercase, it can be converted to uppercase by subtracting `32`.

## Algorithm Steps

* Read the input string
* Check if the first character is lowercase
* Convert it to uppercase if required
* Print the modified string

## Visual Walkthrough

Input:

```
hello
```

ASCII value of `'h'`:

```
104
```

After conversion:

```
104 - 32 = 72 → 'H'
```

Result:

```
Hello
```

## Complexity Analysis

### Time Complexity

O(1)
Only one character is processed.

### Space Complexity

O(1)
No additional memory is used.

## Solution Explanation

The program examines the first character of the string.
If it is a lowercase letter (ASCII value greater than `92`), it converts it to uppercase by subtracting `32`.

All remaining characters are left unchanged, satisfying the problem requirements efficiently.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Input string
    string s;
    cin >> s;

    // Check if the first character is lowercase
    // ASCII value of 'a' is 97, 'A' is 65
    // Difference between lowercase and uppercase is 32
    if (s[0] > 92) {
        s[0] -= 32;
    }

    // Output the modified string
    cout << s << endl;

    return 0;
}
```

## Test Cases Analysis

| Input  | First Character | Output |
| ------ | --------------- | ------ |
| `word` | lowercase       | Word   |
| `Word` | uppercase       | Word   |
| `a`    | lowercase       | A      |
| `Z`    | uppercase       | Z      |

## Edge Cases to Consider

* Single-character strings
* Word already starting with an uppercase letter
* Long words with mixed case characters

## Common Test Cases

* Fully lowercase words
* Already capitalized words
* One-letter words

## Common Mistakes to Avoid

* Modifying characters other than the first
* Incorrect ASCII boundary checks
* Forgetting to print the updated string

## Interview Relevance

* Tests basic string manipulation
* Reinforces ASCII character handling
* Common warm-up problem in interviews

## What This Problem Teaches

* Understanding ASCII value relationships
* Efficient character-level operations
* Precision in modifying specific string positions

## Key Takeaways

* Only the first character needs modification
* ASCII arithmetic is efficient for case conversion
* Simple logic can solve formatting problems cleanly

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on simple string manipulation and character case handling, making it ideal for beginners and interview preparation.