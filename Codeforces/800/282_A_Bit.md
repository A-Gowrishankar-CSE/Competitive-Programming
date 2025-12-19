# A. Bit++

## Platform

Codeforces

## Problem Link

[A. Bit](https://codeforces.com/problemset/problem/282/A)

## Problem Statement

A variable `X` is initially set to `0`.
You are given a sequence of `n` statements. Each statement either increments or decrements the value of `X`.

The possible operations are:

* `++X`
* `X++`
* `--X`
* `X--`

For each statement:

* Increment operations increase `X` by `1`
* Decrement operations decrease `X` by `1`

Your task is to determine the **final value of `X`** after processing all statements.

## Input Format

* The first line contains an integer `n`, the number of statements.
* The next `n` lines each contain a string representing one operation.

## Output Format

Print a single integer representing the final value of `X`.

## Constraints

* `1 ≤ n ≤ 150`
* Each statement is exactly one of: `++X`, `X++`, `--X`, `X--`

## Examples

### Example 1

Input

```
3
++X
X++
X--
```

Explanation

* `++X` → `X = 1`
* `X++` → `X = 2`
* `X--` → `X = 1`

Output

```
1
```

### Example 2

Input

```
1
--X
```

Explanation

* `--X` → `X = -1`

Output

```
-1
```

## Approach

Simple conditional checking with iteration.

## Intuition

The position of the `X` in the statement does **not** affect the result.
Only the presence of `++` or `--` matters.

* If the statement contains `++`, increment the counter.
* Otherwise, decrement the counter.

## Algorithm Steps

* Read the number of statements `n`
* Initialize a variable `ans` to `0`
* For each statement:

  * Read the string
  * If it represents an increment, increase `ans`
  * Otherwise, decrease `ans`
* Output the final value of `ans`

## Visual Walkthrough

Input:

```
++X
X++
X--
```

Step-by-step evaluation:

```
Initial X = 0

++X  → increment → X = 1
X++  → increment → X = 2
X--  → decrement → X = 1
```

Final result:

```
X = 1
```

Key observation:

```
"++X" and "X++" → same effect
"--X" and "X--" → same effect
```

## Complexity Analysis

### Time Complexity

O(n)
Each statement is processed exactly once.

### Space Complexity

O(1)
Only a few variables are used regardless of input size.

## Solution Explanation

The program reads each operation as a string and compares it against the two increment patterns.
If the statement matches either `"++X"` or `"X++"`, the value is incremented.
All other valid cases are decrement operations.

This direct string comparison approach keeps the solution simple and efficient.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of operations to be performed
    int n;

    // Variable to store the final value of X
    int ans = 0;

    // Read number of statements
    cin >> n;

    // Process each statement
    while (n--) {

        // Read the operation as a string
        string s;
        cin >> s;

        // Check for increment operations
        // Both "++X" and "X++" increase the value by 1
        if (s == "++X" || s == "X++") {
            ans++;
        }
        // All remaining valid operations are decrement operations
        else {
            ans--;
        }
    }

    // Output the final value of X
    cout << ans << endl;

    return 0;
}
```

## Test Cases Analysis

| Input | Operations    | Expected Output   |
| ----- | ------------- | ----------------- |
| `1`   | `++X`         | `1`               |
| `1`   | `--X`         | `-1`              |
| `3`   | `++X X++ X--` | `1`               |
| `150` | Mixed         | Correct final sum |

## Edge Cases to Consider

* All operations are decrements
* All operations are increments
* Minimum input size (`n = 1`)

## Common Test Cases

* Alternating increment and decrement
* Multiple consecutive increments
* Multiple consecutive decrements

## Common Mistakes to Avoid

* Treating `++X` and `X++` differently
* Incorrect string comparison
* Forgetting to initialize the counter

## Interview Relevance

* Tests basic string handling
* Evaluates conditional logic
* Common beginner interview problem

## What This Problem Teaches

* Logical interpretation of operations
* Efficient handling of simple input patterns
* Importance of ignoring irrelevant syntax details

## Key Takeaways

* Operation placement does not affect the result
* Clear condition checks simplify the solution
* String comparison can be sufficient for control flow

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on understanding problem statements accurately rather than complex algorithms.