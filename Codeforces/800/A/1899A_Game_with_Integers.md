# A. Game with Integers

## Platform

Codeforces

## Problem Link

[A. Game with Integers](https://codeforces.com/problemset/problem/1749/A)

## Problem Statement

Two players, **First** and **Second**, play a game with an integer `n`.

They take turns making moves according to the game rules.
Your task is to determine **who wins the game** assuming both players play optimally.

The output depends only on the value of `n`.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each test case contains a single integer:

```
n
```

## Output Format

For each test case, print:

* `"First"` if the first player wins
* `"Second"` if the second player wins

Each answer should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ n ≤ 10^9`

## Examples

### Example 1

Input

```
4
1
2
3
4
```

Explanation

* `n = 1` → First wins
* `n = 2` → First wins
* `n = 3` → Second wins
* `n = 4` → First wins

Output

```
First
First
Second
First
```

### Example 2

Input

```
2
6
7
```

Explanation

* `n = 6` → Second wins
* `n = 7` → First wins

Output

```
Second
First
```

## Approach

**Mathematical Observation Using Modulo**

## Intuition

The game outcome follows a repeating pattern based on `n % 3`.

* If `n` is divisible by `3`, the **second player** always wins
* Otherwise, the **first player** always wins

This pattern emerges from analyzing small values of `n` and observing optimal play.

## Pattern Analysis

| n | n % 3 | Winner |
| - | ----- | ------ |
| 1 | 1     | First  |
| 2 | 2     | First  |
| 3 | 0     | Second |
| 4 | 1     | First  |
| 5 | 2     | First  |
| 6 | 0     | Second |

The pattern repeats every 3 numbers.

## Algorithm Steps

* Read the number of test cases
* For each test case:

  * Read integer `n`
  * If `n % 3 == 0`, print `"Second"`
  * Otherwise, print `"First"`

## Visual Walkthrough

Test case:

```
n = 9
```

Calculation:

```
9 % 3 = 0
```

Output:

```
Second
```

Another case:

```
n = 10
```

Calculation:

```
10 % 3 = 1
```

Output:

```
First
```

## Complexity Analysis

### Time Complexity

O(t)

Each test case is processed in constant time.

### Space Complexity

O(1)

No additional data structures are used.

## Solution Explanation

The solution leverages a mathematical observation instead of simulating the game.
By checking whether `n` is divisible by `3`, it directly determines the winner.

This ensures maximum efficiency even for very large values of `n`.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while (t--) {

        // Read the integer n
        int n;
        cin >> n;

        // If n is divisible by 3, the second player wins.
        // Otherwise, the first player wins.
        cout << (n % 3 ? "First\n" : "Second\n");
    }

    return 0;
}
```

## Test Cases Analysis

| n | n % 3 | Winner |
| - | ----- | ------ |
| 1 | 1     | First  |
| 2 | 2     | First  |
| 3 | 0     | Second |
| 6 | 0     | Second |
| 7 | 1     | First  |

## Edge Cases to Consider

* `n = 1`
* Very large values of `n`
* Multiple test cases

## Common Test Cases

* Values divisible by 3
* Values not divisible by 3

## Common Mistakes to Avoid

* Attempting to simulate the game
* Using unnecessary loops
* Forgetting newline formatting in output

## Interview Relevance

* Demonstrates pattern recognition
* Tests mathematical reasoning
* Encourages optimal problem-solving approaches

## What This Problem Teaches

* Observing patterns before coding
* Using modulo arithmetic effectively
* Avoiding unnecessary simulation

## Key Takeaways

* Many game problems reduce to modular patterns
* Simple math can replace complex logic
* Optimal solutions are often short and elegant

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on recognizing patterns and applying basic modular arithmetic, making it suitable for beginners and competitive programming practice.