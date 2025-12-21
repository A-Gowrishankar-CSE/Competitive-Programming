# A. Nearly Lucky Number

## Platform

Codeforces

## Problem Link

[A. Nearly Lucky Number](https://codeforces.com/problemset/problem/110/A)

## Problem Statement

A number is considered **lucky** if it contains only the digits `4` and `7`.

A number is considered **nearly lucky** if the **count of lucky digits** (`4` and `7`) in it is itself a **lucky number**.

Given a number as a string, determine whether it is **nearly lucky**.

## Input Format

* A single string `s` representing the number.

## Output Format

* Print `YES` if the number is nearly lucky.
* Print `NO` otherwise.

## Constraints

* `1 ≤ length(s) ≤ 100`
* The string contains only digits (`0`–`9`)

## Examples

### Example 1

Input

```
40047
```

Explanation
Lucky digits in the number:

```
4, 4, 7 → count = 3
```

Since `3` is not a lucky number (`4` or `7`), the number is not nearly lucky.

Output

```
NO
```

---

### Example 2

Input

```
447774
```

Explanation
Lucky digits:

```
4, 4, 7, 7, 7, 4 → count = 6
```

Since `6` is not a lucky number, the output is:

Output

```
NO
```

---

### Example 3

Input

```
444447
```

Explanation
Lucky digits:

```
4, 4, 4, 4, 4, 7 → count = 6
```

Output

```
NO
```

---

### Example 4

Input

```
7744
```

Explanation
Lucky digits count:

```
4
```

Since `4` is a lucky number:

Output

```
YES
```

---

## Approach

Character counting.

## Intuition

* Only digits `4` and `7` matter.
* The actual number value is irrelevant; only the **count** of lucky digits is checked.
* If the count equals `4` or `7`, the number is nearly lucky.

## Algorithm Steps

* Read the number as a string
* Count digits equal to `'4'` or `'7'`
* Check if the count is `4` or `7`
* Print the result

## Visual Walkthrough

Input:

```
1004477
```

Lucky digits found:

```
4, 4, 7, 7 → count = 4
```

Decision:

```
4 → lucky → YES
```

## Complexity Analysis

### Time Complexity

O(n)
Each digit is examined once.

### Space Complexity

O(1)
Only a counter variable is used.

## Solution Explanation

The solution traverses the input string and increments a counter whenever a `'4'` or `'7'` is encountered.
After the traversal, the counter is checked against the values `4` and `7`.

If the count matches either value, the number is considered nearly lucky.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

int main() {

    // Input number as a string
    string s;
    cin >> s;

    // Counter for lucky digits ('4' and '7')
    int countLucky = 0;

    // Alternative approach using STL (commented):
    // countLucky = count(s.begin(), s.end(), '4')
    //            + count(s.begin(), s.end(), '7');

    // Count lucky digits manually
    for (char ch : s) {
        if (ch == '4' || ch == '7') {
            countLucky++;
        }
    }

    // If the count itself is a lucky number (4 or 7),
    // print YES, otherwise print NO
    cout << (countLucky == 4 || countLucky == 7 ? "YES" : "NO") << endl;

    return 0;
}
```

## Test Cases Analysis

| Input     | Lucky Digit Count | Output |
| --------- | ----------------- | ------ |
| `4`       | 1                 | NO     |
| `47`      | 2                 | NO     |
| `7744`    | 4                 | YES    |
| `4477774` | 7                 | YES    |
| `12345`   | 1                 | NO     |

## Edge Cases to Consider

* No lucky digits present
* All digits are lucky digits
* Very long input number

## Common Test Cases

* Mixed digit numbers
* Numbers with only one lucky digit
* Numbers with exactly 4 or 7 lucky digits

## Common Mistakes to Avoid

* Checking if the number itself is lucky instead of the count
* Forgetting to count both `4` and `7`
* Treating the input as an integer instead of a string

## Interview Relevance

* Tests string traversal
* Reinforces conditional counting
* Common beginner-level digit manipulation problem

## What This Problem Teaches

* Separating problem definition from implementation
* Importance of counting-based logic
* Effective use of character iteration

## Key Takeaways

* Only the count of special digits matters
* String-based processing avoids numeric overflow
* Simple conditional checks solve the problem efficiently

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It emphasizes digit counting and conditional logic, making it suitable for beginners and competitive programming practice.