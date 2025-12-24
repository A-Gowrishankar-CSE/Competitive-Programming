# B. Drinks

## Platform

Codeforces

## Problem Link

[B. Drinks](https://codeforces.com/problemset/problem/200/B)

## Problem Statement

Little Vasya loves orange juice. He has `n` drinks, each containing a certain percentage of orange juice.

Vasya wants to make a cocktail by mixing all the drinks together.
Your task is to calculate the **percentage of orange juice** in the final mixture.

The percentage is defined as the **average** of the given percentages.

## Input Format

* The first line contains an integer `n`, the number of drinks
* The second line contains `n` integers, each representing the percentage of orange juice in a drink

## Output Format

Print a floating-point number representing the percentage of orange juice in the mixture.

The answer must be printed with **high precision**.

## Constraints

* `1 ≤ n ≤ 100`
* `0 ≤ p[i] ≤ 100`

## Examples

### Example 1

Input

```
3
50 50 100
```

Explanation

Total percentage sum:

```
50 + 50 + 100 = 200
```

Average percentage:

```
200 / 3 = 66.666666666666
```

Output

```
66.666666666666
```

### Example 2

Input

```
4
0 0 0 0
```

Explanation

All drinks contain 0% orange juice.

Output

```
0.000000000000
```

## Approach

Simple average calculation with floating-point precision.

## Intuition

Since all drinks are mixed equally, the resulting orange juice percentage is simply the **arithmetic mean** of the given percentages.

To ensure accurate results, floating-point division and controlled output precision are required.

## Algorithm Steps

* Read integer `n`
* Initialize a variable `sum` to store total percentage
* For each drink:

  * Read percentage `p`
  * Add `p` to `sum`
* Compute `sum / n` using floating-point division
* Print the result with fixed precision

## Visual Walkthrough

Input percentages:

```
30 40 50
```

Sum:

```
30 + 40 + 50 = 120
```

Average:

```
120 / 3 = 40.0
```

Final output:

```
40.000000000000
```

## Complexity Analysis

### Time Complexity

**O(n)**
Each drink is processed once.

### Space Complexity

**O(1)**
Only constant extra variables are used.

## Solution Explanation

The solution accumulates the total percentage of orange juice from all drinks.

By dividing the total by the number of drinks using floating-point arithmetic, the average percentage is obtained.

The use of `fixed` and `setprecision(12)` ensures that the output meets the precision requirements specified by the problem.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
#include <iomanip>
using namespace std;

int main() {

    // Number of drinks
    int n;

    // Sum of orange juice percentages
    int sum = 0;

    // Read number of drinks
    cin >> n;

    // Read percentages and accumulate sum
    for (int i = 0; i < n; i++) {
        int p;
        cin >> p;
        sum += p;
    }

    // Calculate and print the average percentage
    cout << fixed << setprecision(12)
         << (double) sum / n << endl;

    return 0;
}
```

## Test Cases Analysis

| n | Percentages     | Output           |
| - | --------------- | ---------------- |
| 1 | 100             | 100.000000000000 |
| 3 | 50 50 100       | 66.666666666666  |
| 4 | 0 0 0 0         | 0.000000000000   |
| 5 | 20 40 60 80 100 | 60.000000000000  |

## Edge Cases to Consider

* Only one drink
* All drinks with 0% juice
* All drinks with 100% juice

## Common Test Cases

* Mixed percentages
* Uniform percentages
* Minimum input size

## Common Mistakes to Avoid

* Using integer division instead of floating-point division
* Not setting sufficient output precision
* Forgetting to include `<iomanip>`

## Interview Relevance

* Tests understanding of averages
* Evaluates floating-point precision handling
* Common arithmetic problem in interviews

## What This Problem Teaches

* Importance of precision in floating-point output
* Correct use of type casting
* Simple aggregation and averaging logic

## Key Takeaways

* Always use floating-point arithmetic for averages
* Output formatting matters in competitive programming
* Simple problems still require careful implementation

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on basic arithmetic and precision handling, making it ideal for beginners and quick practice.