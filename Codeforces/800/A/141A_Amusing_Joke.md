# A_Amusing_Joke

## Platform

Codeforces

## Problem Link

[A. Amusing Joke](https://codeforces.com/problemset/problem/141/A)

## Problem Statement

When Dima and his friends were playing jokes, they wrote the name of one friend on a piece of paper, then the name of another friend on another piece of paper, and finally mixed up all the letters from both names and wrote them on a third piece of paper.

You are given:

* The name of the **guest**
* The name of the **host**
* The string of letters written on the third piece of paper (the **pile**)

Your task is to determine whether the pile of letters can be formed **exactly** by rearranging the letters of the guest’s and host’s names.

## Input Format

* The first line contains a string `guest`
* The second line contains a string `host`
* The third line contains a string `pile`

All strings consist only of **uppercase English letters**.

## Output Format

* Print `"YES"` if the pile is a valid rearrangement
* Print `"NO"` otherwise

## Constraints

* `1 ≤ |guest|, |host| ≤ 100`
* `|pile| = |guest| + |host|`
* All characters are uppercase letters `A` to `Z`

## Examples

### Example 1

Input

```
ANN
BOB
ANNBOB
```

Explanation

Letters from `guest + host`

```
ANN + BOB → ANNBOB
```

Pile matches exactly.

Output

```
YES
```

---

### Example 2

Input

```
TOM
JERRY
TOMJERYY
```

Explanation

The pile contains an extra `'Y'`.

Output

```
NO
```

---

### Example 3

Input

```
ABC
DEF
FEDCBA
```

Explanation

All letters match in correct counts.

Output

```
YES
```

## Approach

**Frequency counting using a fixed-size array**

## Intuition

Since all characters are uppercase English letters, we only need to track **26 possible characters**.

The idea is simple:

* Count how many times each letter appears in the pile
* Subtract the counts for letters appearing in the guest and host names
* If all final counts are zero, the pile is a valid rearrangement

## Algorithm Steps

* Read strings `guest`, `host`, and `pile`
* Create an integer array of size 26 initialized to zero
* For each character in `pile`, increment its frequency
* For each character in `guest`, decrement its frequency
* For each character in `host`, decrement its frequency
* Check the frequency array:

  * If any value is non-zero, print `"NO"`
  * Otherwise, print `"YES"`

## Visual Walkthrough

### Case 1

Input

```
guest = ANN
host  = BOB
pile  = ANNBOB
```

Frequency changes

```
Pile   → A:+1 N:+2 B:+2 O:+1
Guest  → A:-1 N:-2
Host   → B:-1 O:-1 B:-1
Final  → all zeros
```

Result

```
YES
```

---

### Case 2

Input

```
guest = TOM
host  = JERRY
pile  = TOMJERYY
```

Frequency changes

```
Extra Y remains
```

Result

```
NO
```

## Complexity Analysis

### Time Complexity

**O(n)**
Where `n` is the total length of the strings.

### Space Complexity

**O(1)**
A fixed-size array of 26 integers is used.

## Solution Explanation

The solution leverages the fact that character order does not matter — only frequency matters.

By incrementing counts for the pile and decrementing for the guest and host, the array should end with all zeros if and only if the pile contains exactly the same letters in the same quantities.

This ensures correctness with minimal overhead.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    string guest, host, pile;
    cin >> guest >> host >> pile;

    // Frequency array for uppercase letters
    int f[26] = { 0 };

    // Count letters in pile
    for (char ch : pile)
        f[ch - 'A']++;

    // Remove letters of guest
    for (char ch : guest)
        f[ch - 'A']--;

    // Remove letters of host
    for (char ch : host)
        f[ch - 'A']--;

    // Check if all counts are zero
    for (int i : f) {
        if (i != 0) {
            cout << "NO\n";
            return 0;
        }
    }

    cout << "YES\n";
    return 0;
}
```

## Test Cases Analysis

| Guest | Host  | Pile     | Output |
| ----- | ----- | -------- | ------ |
| ANN   | BOB   | ANNBOB   | YES    |
| TOM   | JERRY | TOMJERYY | NO     |
| ABC   | DEF   | FEDCBA   | YES    |
| A     | B     | AB       | YES    |

## Edge Cases to Consider

* Single-character names
* Repeated characters
* Extra or missing characters in the pile
* Correct letters but incorrect counts

## Common Mistakes to Avoid

* Comparing sorted strings unnecessarily
* Ignoring character frequency
* Forgetting to check all 26 letters

## Interview Relevance

* Tests string manipulation and counting
* Evaluates understanding of frequency arrays
* Common verification problem

## What This Problem Teaches

* Order-independent string comparison
* Efficient character frequency tracking
* Use of fixed-size arrays for alphabet problems

## Key Takeaways

* Rearrangement problems reduce to frequency comparison
* Fixed-size arrays are faster than maps for alphabets
* Always validate counts, not just total length

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It emphasizes basic string processing and frequency counting, making it ideal for beginners and early competitive programming practice.