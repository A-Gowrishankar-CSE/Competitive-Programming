# A_Array_Coloring

## Platform

Codeforces

## Problem Link

[A. Array Coloring](https://codeforces.com/problemset/problem/1857/A)

## Problem Statement

You are given multiple test cases.
In each test case, an array of integers is provided.

You want to color each element of the array either **red** or **blue** such that the **sum of red elements is equal to the sum of blue elements**.

Determine whether such a coloring is possible.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * An integer `n`, the size of the array
  * A line containing `n` integers representing the array elements

## Output Format

For each test case:

* Print `"YES"` if the array can be colored as required
* Otherwise, print `"NO"`

Each result should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ n ≤ 100`
* `0 ≤ array[i] ≤ 100`

## Examples

### Example 1

Input

```
3
4
1 1 2 2
3
1 2 3
2
5 5
```

Explanation

* Test case 1:

  * Total sum = `6`
  * Can be split into `3` and `3` → possible
* Test case 2:

  * Total sum = `6`
  * Can be split into `3` and `3` → possible
* Test case 3:

  * Total sum = `10`
  * Can be split into `5` and `5` → possible

Output

```
YES
YES
YES
```

### Example 2

Input

```
1
3
1 1 1
```

Explanation

* Total sum = `3`, which is odd
* Equal split is impossible

Output

```
NO
```

## Approach (Algorithm Name / Type)

**Parity Check Using Aggregate Sum**

This approach determines feasibility based on the parity (odd or even) of the total array sum.

## Intuition

To split the array into two groups with equal sum:

* The **total sum must be even**
* If the sum is odd, it cannot be divided into two equal integers

The actual distribution of elements does not matter once the total sum’s parity is known.

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read the array size `n`
  * Compute the sum of all elements
  * If the sum is even, print `"YES"`
  * Otherwise, print `"NO"`

## Visual Walkthrough

### Test Case 1

Input:

```
1 1 2 2
```

Total sum:

```
1 + 1 + 2 + 2 = 6
```

Evaluation:

```
6 is even → possible
```

Result:

```
YES
```

---

### Test Case 2

Input:

```
1 1 1
```

Total sum:

```
1 + 1 + 1 = 3
```

Evaluation:

```
3 is odd → impossible
```

Result:

```
NO
```

---

### Test Case 3

Input:

```
5 5
```

Total sum:

```
10
```

Evaluation:

```
Even → possible
```

Result:

```
YES
```

## Complexity Analysis

### Time Complexity

**O(n)** per test case

Each element is read and added once.

### Space Complexity

**O(1)**

Only a running sum variable is used.

## Solution Explanation

The solution relies on a mathematical property rather than explicit coloring.

If the total sum of the array is even, it is always possible to split it into two equal halves. If the sum is odd, such a split is impossible regardless of how elements are grouped.

This makes the solution both efficient and elegant.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of test cases
    int t;
    cin >> t;

    // Process each test case
    while (t--) {

        // Size of the array
        int n;
        cin >> n;

        // Variable to store the sum of elements
        int sum = 0;

        // Read all elements and calculate the sum
        while (n--) {
            int value;
            cin >> value;
            sum += value;
        }

        // If total sum is even, equal coloring is possible
        if (sum & 1) {
            cout << "NO\n";
        } else {
            cout << "YES\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Array     | Total Sum | Parity | Output |
| --------- | --------- | ------ | ------ |
| `1 1 2 2` | 6         | Even   | YES    |
| `1 2 3`   | 6         | Even   | YES    |
| `1 1 1`   | 3         | Odd    | NO     |
| `5 5`     | 10        | Even   | YES    |

## Edge Cases to Consider

* Single element array
* All zero elements
* Large values with even total sum

## Common Test Cases

* Arrays with all equal values
* Mixed even and odd values
* Arrays with minimum size

## Common Mistakes to Avoid

* Attempting to simulate coloring unnecessarily
* Forgetting to reset the sum for each test case
* Incorrect parity check

## Interview Relevance

* Tests understanding of parity and invariants
* Encourages mathematical reasoning over brute force
* Common problem for logical simplification

## What This Problem Teaches

* Recognizing when a condition is both necessary and sufficient
* Simplifying problems using mathematical properties
* Writing minimal and efficient code

## Key Takeaways

* Equal partition requires an even total sum
* Parity checks can replace complex logic
* Efficient solutions often come from problem insight

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on identifying a key mathematical condition rather than complex data structures or algorithms, making it ideal for beginners and quick assessments.