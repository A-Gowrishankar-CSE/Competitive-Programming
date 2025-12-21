# A. Beautiful Year

## Platform

Codeforces

## Problem Link

[A. Beautiful Year](https://codeforces.com/problemset/problem/271/A)

## Problem Statement

A year is called **beautiful** if all its digits are **distinct**.

You are given an integer representing a year.
Your task is to find the **next year strictly greater than the given year** that is beautiful.

## Input Format

* A single integer `year`

## Output Format

Print the next beautiful year.

## Constraints

* `1000 ≤ year ≤ 9000`
* The result is guaranteed to exist

## Examples

### Example 1

Input

```
1987
```

Explanation

The next years are checked sequentially:

* 1988 → digits repeat (`8`)
* 1989 → digits repeat (`9`)
* 1990 → digits repeat (`9`)
* 2013 → all digits are distinct

Output

```
2013
```

### Example 2

Input

```
2013
```

Explanation

The next year with all distinct digits is `2014`.

Output

```
2014
```

## Approach

Digit frequency checking using a fixed-size boolean array.

## Intuition

To determine whether a year is beautiful, we need to ensure that **no digit appears more than once**.

Since digits range from `0` to `9`, a boolean array of size 10 is sufficient to track whether a digit has already appeared.

Starting from the year immediately after the given one, we increment year-by-year until we find a year whose digits are all distinct.

## Algorithm Steps

* Read the input year
* Increment the year by 1
* For each candidate year:

  * Extract digits one by one
  * Mark digits as visited
  * If a digit repeats, reject the year
* Stop when a valid beautiful year is found
* Print the year

## Visual Walkthrough

Given year: `1987`

Checking `1988`

```
Digits: 1, 9, 8, 8
Digit 8 repeats → not beautiful
```

Checking `2013`

```
Digits: 2, 0, 1, 3
All digits unique → beautiful year found
```

## Complexity Analysis

### Time Complexity

**O(Y × D)**
Where:

* `Y` is the number of years checked (small, bounded)
* `D` is the number of digits (at most 4)

Effectively constant time due to tight constraints.

### Space Complexity

**O(1)**
A fixed-size boolean array of length 10 is used.

## Solution Explanation

The solution separates the digit uniqueness logic into a helper function.

The helper function uses a boolean array to record which digits have already appeared. If any digit is encountered more than once, the year is rejected.

The main function increments the year until a valid beautiful year is found and then prints it.

This design ensures clarity, efficiency, and adherence to the problem constraints.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

// Function to check if all digits of a number are distinct
bool isDistinct(int n) {

    // Boolean array to track used digits
    bool used[10] = {false};

    // Process each digit
    while (n) {

        int rem = n % 10;

        // If digit already appeared, number is not distinct
        if (used[rem])
            return false;

        // Mark digit as used
        used[rem] = true;

        n /= 10;
    }

    // All digits are distinct
    return true;
}

int main() {

    // Input year
    int year;
    cin >> year;

    // Increment year until a beautiful year is found
    while (++year) {

        if (isDistinct(year)) {
            cout << year << endl;
            break;
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Input Year | Output Year | Reasoning                    |
| ---------- | ----------- | ---------------------------- |
| 1987       | 2013        | Next year with unique digits |
| 2013       | 2014        | Immediate next valid year    |
| 999        | 1023        | All digits become distinct   |
| 1234       | 1235        | Simple increment works       |

## Edge Cases to Consider

* Years with all digits identical
* Years containing repeated zeros
* Transition across centuries (e.g., 1999 → 2013)

## Common Test Cases

* Already beautiful years
* Years with three repeated digits
* Boundary values near 1000

## Common Mistakes to Avoid

* Forgetting to reset digit tracking for each year
* Not checking years strictly greater than the input
* Using inefficient string conversions unnecessarily

## Interview Relevance

* Tests digit manipulation skills
* Reinforces use of helper functions
* Evaluates loop control and termination logic

## What This Problem Teaches

* How to analyze numbers digit by digit
* Effective use of fixed-size frequency arrays
* Clean separation of logic into reusable functions

## Key Takeaways

* Small constraints allow simple brute-force solutions
* Digit-based problems often benefit from frequency tracking
* Clear logic improves correctness and maintainability

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on basic number manipulation and logical checks, making it ideal for beginners and interview warm-up practice.
