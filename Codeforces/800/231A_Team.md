# A_Team

## Platform

Codeforces

## Problem Link

[A. Team](https://codeforces.com/problemset/problem/231/A)

## Problem Statement

A group of three friends is working on programming problems. For each problem, every friend decides whether they are confident enough to solve it.

A problem will be solved **only if at least two of the three friends are confident**.

Given the confidence decisions for multiple problems, determine how many problems the team will solve.

## Input Format

* The first line contains an integer `n`, the number of problems.
* The next `n` lines each contain three integers `a`, `b`, and `c`.

  * Each value is either `0` (not confident) or `1` (confident).

## Output Format

Print a single integer representing the number of problems the team will solve.

## Constraints

* `1 ≤ n ≤ 1000`
* `a, b, c ∈ {0, 1}`

## Examples

### Example 1

Input

```
3
1 1 0
1 1 1
1 0 0
```

Explanation

* Problem 1: Two members are confident → solved
* Problem 2: All three are confident → solved
* Problem 3: Only one member is confident → not solved

Output

```
2
```

### Example 2

Input

```
1
0 0 0
```

Explanation
No member is confident, so the problem is not solved.

Output

```
0
```

## Approach

Simple iteration and counting based on conditional checks.

## Intuition

Each problem is independent.
For every problem, count how many team members are confident.
If the sum of confidence values is **greater than 1**, the problem is solved.

## Algorithm Steps

* Read the number of problems `n`.
* Initialize a counter to track solved problems.
* For each problem:

  * Read three integers.
  * Add them.
  * If the sum is at least 2, increment the counter.
* Output the counter.

## Visual Walkthrough

Example input:

```
1 1 0
```

Interpretation:

```
Member 1 → confident
Member 2 → confident
Member 3 → not confident
```

Confidence sum:

```
1 + 1 + 0 = 2  → problem solved
```

Decision rule:

```
Sum ≥ 2  → solved
Sum < 2  → not solved
```

## Complexity Analysis

### Time Complexity

O(n)
Each problem is processed once.

### Space Complexity

O(1)
Only constant extra variables are used.

## Solution Explanation

The solution reads input values, evaluates each problem independently, and increments a counter whenever at least two team members are confident. This approach is efficient, clear, and directly matches the problem requirements.

## Full Solution

### Java Implementation

```java
import java.util.*;

public class A_Team {

    public static void main(String[] args) {

        // Scanner object to read input from standard input
        Scanner sc = new Scanner(System.in);

        // Number of problems
        int n = sc.nextInt();

        // Counter to store how many problems are solved
        int count = 0;

        // Loop through all problems
        while (n-- > 0) {

            // Read confidence values of the three team members
            int a = sc.nextInt();
            int b = sc.nextInt();
            int c = sc.nextInt();

            // If at least two members are confident,
            // then the problem will be solved
            if (a + b + c > 1) {
                count++;
            }
        }

        // Print the total number of solved problems
        System.out.println(count);
    }
}
```

### C++

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of problems
    int n;

    // Counter for solved problems
    int count = 0;

    // Read number of problems
    cin >> n;

    // Process each problem
    while (n--) {

        // Confidence values of the three team members
        int a, b, c;
        cin >> a >> b >> c;

        // If at least two members are confident,
        // increment the solved problem counter
        if (a + b + c > 1) {
            count++;
        }
    }

    // Output the result
    cout << count << endl;

    return 0;
}
```

## Test Cases Analysis

| Input Size | Confidence Pattern | Expected Output         |
| ---------- | ------------------ | ----------------------- |
| n = 1      | 1 1 0              | 1                       |
| n = 1      | 0 0 1              | 0                       |
| n = 3      | Mixed              | Count of valid problems |
| n = 1000   | All valid          | 1000                    |

## Edge Cases to Consider

* All team members say `0` for every problem
* Exactly two members say `1`
* Minimum input size (`n = 1`)

## Common Test Cases

* Problems where exactly two members agree
* Problems where all three agree
* Problems where only one member agrees

## Common Mistakes to Avoid

* Using `>= 3` instead of `>= 2`
* Forgetting to reset or initialize the counter
* Incorrect loop condition

## Interview Relevance

* Tests basic conditional logic
* Evaluates input handling and iteration
* Common warm-up problem in interviews

## What This Problem Teaches

* Translating problem statements into simple logic
* Efficient counting techniques
* Clean input/output handling

## Key Takeaways

* Simple conditions can solve seemingly larger problems
* Always map problem rules directly to code logic
* Readability matters even for easy problems

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on logical reasoning rather than complex algorithms and is ideal for beginners and interview warm-ups.