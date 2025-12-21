# A. Anton and Danik

## Platform

Codeforces

## Problem Link

[A. Anton and Danik](https://codeforces.com/problemset/problem/734/A)

## Problem Statement

Anton and Danik are playing a game consisting of `n` rounds.

* In each round, either **Anton** wins (`'A'`) or **Danik** wins (`'D'`)
* The result of all rounds is given as a string of length `n`

Determine the overall winner:

* Print `"Anton"` if Anton wins more rounds
* Print `"Danik"` if Danik wins more rounds
* Print `"Friendship"` if both win the same number of rounds

## Input Format

* The first line contains an integer `n`, the number of rounds
* The second line contains a string `s` of length `n` consisting of characters `'A'` and `'D'`

## Output Format

* Print `"Anton"`, `"Danik"`, or `"Friendship"`

## Constraints

* `1 ≤ n ≤ 100000`
* `s[i] ∈ { 'A', 'D' }`

## Examples

### Example 1

Input

```
6
ADAAAA
```

Explanation
Anton wins 5 rounds, Danik wins 1 round.

Output

```
Anton
```

---

### Example 2

Input

```
7
DDDAAAD
```

Explanation
Anton wins 3 rounds, Danik wins 4 rounds.

Output

```
Danik
```

---

### Example 3

Input

```
4
ADDA
```

Explanation
Anton wins 2 rounds, Danik wins 2 rounds.

Output

```
Friendship
```

---

## Approach

Two different approaches are demonstrated:

* **Approach 1**: Direct counting
* **Approach 2**: Boyer–Moore Majority Voting Algorithm

Both approaches correctly solve the problem under given constraints.

---

## Intuition

* The problem is fundamentally about determining which character (`'A'` or `'D'`) appears more frequently.
* Since only two outcomes are possible, simple counting is sufficient.
* Alternatively, the majority voting algorithm can be used to identify a dominant winner efficiently.

---

## Algorithm Steps

### Approach 1 – Direct Counting

* Read `n` and string `s`
* Count occurrences of `'A'` and `'D'`
* Compare the counts
* Print the appropriate result

### Approach 2 – Majority Voting

* Assume the first character as the majority
* Traverse the string using Boyer–Moore logic
* Adjust majority count based on matches and mismatches
* Decide the winner based on final majority state

---

## Visual Walkthrough

Input:

```
ADDAA
```

### Approach 1

```
A → 3
D → 2
Result → Anton
```

### Approach 2

```
Majority evolves while scanning
Final majority → 'A'
Result → Anton
```

---

## Complexity Analysis

### Time Complexity

* **Approach 1**: O(n)
* **Approach 2**: O(n)

### Space Complexity

* **Approach 1**: O(1)
* **Approach 2**: O(1)

---

## Solution Explanation

### Approach 1 Explanation

This approach explicitly counts the number of wins for Anton and Danik by iterating through the string.
It is simple, readable, and optimal for the given constraints.

### Approach 2 Explanation

This approach applies the **Boyer–Moore Majority Voting Algorithm**, which identifies a potential majority element using constant space.
If a true majority exists, it will remain as the final candidate.

In this problem:

* If no majority remains, the result is `"Friendship"`
* Otherwise, the remaining candidate determines the winner

---

## Full Solution

### C++ Implementation – Approach 1 (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of rounds
    int n;

    // Counters for Anton and Danik
    int a = 0, d = 0;

    // Result string
    string s;

    // Read input
    cin >> n >> s;

    // Count wins
    for (char ch : s) {
        if (ch == 'A')
            a++;
        else
            d++;
    }

    // Decide winner
    cout << (a == d ? "Friendship" : a > d ? "Anton" : "Danik") << endl;

    return 0;
}
```

---

### C++ Implementation – Approach 2 (Boyer–Moore, Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of rounds
    int n;

    // Majority count initialization
    int majorityCount = 1;

    // Result string
    string s;

    // Read input
    cin >> n >> s;

    // Assume first character as majority
    char majority = s[0];

    // Boyer–Moore Majority Voting Algorithm
    for (int i = 1; i < n; i++) {

        if (majorityCount == 0) {
            majority = s[i];
            majorityCount = 1;
        }
        else {
            if (s[i] == majority)
                majorityCount++;
            else
                majorityCount--;
        }
    }

    // Output result
    cout << (majorityCount == 0 ? "Friendship"
                                : majority == 'A' ? "Anton" : "Danik") << endl;

    return 0;
}
```

---

## Test Cases Analysis

| Input   | Anton Wins | Danik Wins | Output     |
| ------- | ---------- | ---------- | ---------- |
| `A`     | 1          | 0          | Anton      |
| `D`     | 0          | 1          | Danik      |
| `AD`    | 1          | 1          | Friendship |
| `AADDD` | 2          | 3          | Danik      |
| `AAADD` | 3          | 2          | Anton      |

---

## Edge Cases to Consider

* Only one round
* All rounds won by one player
* Equal number of wins
* Very large `n`

---

## Common Test Cases

* Balanced outcomes
* Strong majority for one player
* Alternating results

---

## Common Mistakes to Avoid

* Forgetting to handle tie condition
* Assuming majority always exists
* Misinterpreting character values

---

## Interview Relevance

* Approach 1 tests basic counting and string traversal
* Approach 2 demonstrates knowledge of majority voting algorithms
* Highlights trade-offs between simplicity and algorithmic elegance

---

## What This Problem Teaches

* Multiple valid approaches can exist for the same problem
* Choosing the simplest correct solution is often best
* Advanced algorithms should be applied judiciously

---

## Key Takeaways

* Counting is sufficient when constraints are small
* Boyer–Moore works efficiently with constant space
* Always handle tie conditions explicitly

---

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It primarily tests string processing and logical comparison, with optional exposure to a classic majority algorithm.