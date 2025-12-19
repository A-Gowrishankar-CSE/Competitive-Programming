# A. Next Round

## Platform

Codeforces

## Problem Link

[A. Next Round](https://codeforces.com/problemset/problem/158/A)

## Problem Statement

A total of `n` participants take part in a contest, and their scores are given in non-increasing order.
The contest advances participants to the next round based on the following rules:

A participant advances if:

* Their score is **positive**, and
* Their score is **greater than or equal to the score of the k-th participant**

Determine how many participants advance to the next round.

## Input Format

* The first line contains two integers `n` and `k`.
* The second line contains `n` integers representing the scores of participants in descending order.

## Output Format

Print a single integer representing the number of participants who advance to the next round.

## Constraints

* `1 ≤ n ≤ 50`
* `1 ≤ k ≤ n`
* `0 ≤ score[i] ≤ 100`
* Scores are given in **non-increasing order**

## Examples

### Example 1

Input

```
8 5
10 9 8 7 7 7 5 5
```

Explanation
The 5th participant has a score of `7`.
All participants with score `≥ 7` and score `> 0` advance.

Valid participants:

```
10, 9, 8, 7, 7, 7
```

Output

```
6
```

---

### Example 2

Input

```
4 2
0 0 0 0
```

Explanation
The k-th participant’s score is `0`.
Since scores must be **positive**, no participant advances.

Output

```
0
```

---

## Approach

Greedy iteration with early termination based on sorted score order.

## Intuition

Because the scores are already sorted in descending order, once a score becomes:

* zero, or
* smaller than the k-th participant’s score

no subsequent participant can qualify.
This allows the loop to terminate early, making the solution efficient and simple.

## Algorithm Steps

* Read `n` and `k`
* Convert `k` to zero-based index
* Store all participant scores
* Traverse the scores from the beginning
* Stop when:

  * score becomes zero, or
  * score is less than `score[k]`
* Count all valid participants
* Output the count

## Visual Walkthrough

Scores:

```
[10, 9, 8, 7, 7, 7, 5, 5]
```

k = 5 → index `4`
k-th score = `7`

Evaluation:

```
10 ≥ 7 → advance
9  ≥ 7 → advance
8  ≥ 7 → advance
7  ≥ 7 → advance
7  ≥ 7 → advance
7  ≥ 7 → advance
5  < 7 → stop
```

Total advanced participants = `6`

## Complexity Analysis

### Time Complexity

O(n)
Each participant is checked once.

### Space Complexity

O(n)
An array is used to store scores.

## Solution Explanation

The solution relies on the fact that scores are sorted in non-increasing order.
By comparing each participant’s score with the k-th participant’s score and checking for positivity, the algorithm efficiently counts all valid participants and exits early when further checks become unnecessary.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of participants (n)
    // Position threshold (k)
    int n, k;

    // Variable to count participants advancing to next round
    int ans = 0;

    // Read n and k
    cin >> n >> k;

    // Convert k to zero-based index
    k--;

    // Array to store scores of participants
    int nums[n];

    // Read participant scores
    for (int i = 0; i < n; i++) {
        cin >> nums[i];
    }

    // Iterate through participant scores
    for (int i = 0; i < n; i++) {

        // Stop if score is zero OR
        // score is less than the k-th participant's score
        if (!nums[i] || nums[i] < nums[k]) {
            break;
        }

        // Valid participant advances
        ans++;
    }

    // Output the total number of participants advancing
    cout << ans;

    return 0;
}
```

## Test Cases Analysis

| Input                | k-th Score | Expected Output | Reasoning                |
| -------------------- | ---------- | --------------- | ------------------------ |
| `8 5` / mixed scores | 7          | 6               | Scores ≥ 7 and > 0       |
| `4 2` / all zeros    | 0          | 0               | Score must be positive   |
| `1 1` / `5`          | 5          | 1               | Single valid participant |
| `5 3` / `3 3 3 0 0`  | 3          | 3               | Stops at first zero      |

## Edge Cases to Consider

* All scores are zero
* k-th participant’s score is zero
* Only one participant
* Multiple participants sharing the k-th score

## Common Test Cases

* Scores with ties at k-th position
* Strictly decreasing scores
* Scores ending with zeros

## Common Mistakes to Avoid

* Forgetting to convert `k` to zero-based indexing
* Counting participants with zero score
* Ignoring early termination logic

## Interview Relevance

* Tests understanding of array traversal
* Reinforces zero-based indexing concepts
* Demonstrates optimization using sorted data

## What This Problem Teaches

* Leveraging sorted input for efficiency
* Proper boundary and condition checks
* Writing clean loop termination logic

## Key Takeaways

* Sorted inputs often allow early exits
* Always validate positivity when required
* Indexing errors are a common source of bugs

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It emphasizes logical conditions and efficient traversal rather than complex algorithms, making it ideal for beginners and competitive programming warm-ups.