# A. Vasya and the Hipster

## Platform

Codeforces

## Problem Link

[A. Vasya and the Hipster](https://codeforces.com/problemset/problem/581/A)

## Problem Statement

Vasya has two types of socks:

* `a` red socks
* `b` blue socks

Each day, Vasya wears **one pair of socks**.
A pair can be:

* **Different-colored**, using one red and one blue sock
* **Same-colored**, using two socks of the same color

Determine:

* The **maximum number of days** Vasya can wear different-colored socks
* The **maximum number of additional days** he can wear same-colored socks afterward

## Input Format

A single line containing two integers:

```
a b
```

## Output Format

Print two integers separated by a space:

* Maximum number of days wearing different-colored socks
* Maximum number of days wearing same-colored socks after that

## Constraints

* `0 ≤ a, b ≤ 1000`

## Examples

### Example 1

Input

```
3 1
```

Explanation

* Different-colored pairs: `min(3, 1) = 1`
* Remaining socks: `2` red
* Same-colored pairs: `2 / 2 = 1`

Output

```
1 1
```

### Example 2

Input

```
4 4
```

Explanation

* Different-colored pairs: `4`
* No socks remain

Output

```
4 0
```

### Example 3

Input

```
0 5
```

Explanation

* No different-colored pairs possible
* Same-colored pairs: `5 / 2 = 2`

Output

```
0 2
```

## Approach

**Greedy Counting Based on Minimum and Difference**

## Intuition

To maximize different-colored sock days, Vasya should always pair one red with one blue.
The maximum such pairs is limited by the smaller count.

After using those, only one color remains.
Every two remaining socks of the same color form one same-colored pair.

## Algorithm Steps

* Read values `a` and `b`
* Compute different-colored days as `min(a, b)`
* Compute remaining socks as `abs(a − b)`
* Compute same-colored days as `(remaining socks) / 2`
* Output both results

## Visual Walkthrough

Input:

```
a = 3, b = 1
```

Different-colored days:

```
min(3, 1) = 1
```

Remaining socks:

```
|3 − 1| = 2
```

Same-colored days:

```
2 / 2 = 1
```

Final result:

```
1 1
```

Another case:

```
a = 0, b = 5
```

Different-colored:

```
0
```

Same-colored:

```
5 / 2 = 2
```

## Complexity Analysis

### Time Complexity

O(1)

Only constant-time arithmetic operations are used.

### Space Complexity

O(1)

No additional data structures are required.

## Solution Explanation

The solution directly applies greedy logic.
First, it maximizes mixed-color pairs by pairing red and blue socks.
Then, it counts how many same-color pairs can be formed from the remaining socks.

This ensures the maximum number of total days.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // a -> number of red socks
    // b -> number of blue socks
    int a, b;
    cin >> a >> b;

    // Maximum days with different-colored socks
    int different = min(a, b);

    // Remaining socks after forming different-colored pairs
    int remaining = abs(a - b);

    // Maximum days with same-colored socks
    int same = remaining / 2;

    // Output results
    cout << different << " " << same;

    return 0;
}
```

## Test Cases Analysis

| Red Socks | Blue Socks | Different Days | Same Days |
| --------- | ---------- | -------------- | --------- |
| 3         | 1          | 1              | 1         |
| 4         | 4          | 4              | 0         |
| 0         | 5          | 0              | 2         |
| 7         | 3          | 3              | 2         |

## Edge Cases to Consider

* One color has zero socks
* Both colors have equal counts
* Very large differences between counts

## Common Test Cases

* Balanced inputs
* One-sided inputs
* Minimal values

## Common Mistakes to Avoid

* Forgetting to divide remaining socks by 2
* Using addition instead of minimum
* Mishandling absolute difference

## Interview Relevance

* Tests greedy strategy
* Evaluates arithmetic reasoning
* Common beginner-level problem

## What This Problem Teaches

* Breaking problems into independent components
* Using simple math to model real-world constraints
* Writing clean and efficient logic

## Key Takeaways

* Pairing strategy matters in optimization problems
* Minimum and difference often reveal optimal solutions
* Constant-time logic can fully solve the problem

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on greedy reasoning and basic arithmetic, making it suitable for beginners and coding interview preparation.