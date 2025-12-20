# A. Bear and Big Brother

## Platform

Codeforces

## Problem Link

[A. Bear and Big Brother](https://codeforces.com/problemset/problem/791/A)

## Problem Statement

Bear Limak and his brother Bob are both bears.

Initially:

* Limak’s weight is `a`
* Bob’s weight is `b`

Every year:

* Limak’s weight becomes **three times** heavier
* Bob’s weight becomes **two times** heavier

Determine the **minimum number of years** required for Limak to become **strictly heavier** than Bob.

## Input Format

* A single line containing two integers `a` and `b`.

## Output Format

* Print a single integer representing the number of years required.

## Constraints

* `1 ≤ a, b ≤ 10`
* `a ≤ b`

## Examples

### Example 1

Input

```
4 7
```

Explanation
Year-by-year growth:

```
Year 1: Limak = 12, Bob = 14
Year 2: Limak = 36, Bob = 28
```

Limak becomes heavier after `2` years.

Output

```
2
```

---

### Example 2

Input

```
1 1
```

Explanation
Year-by-year growth:

```
Year 1: Limak = 3, Bob = 2
```

Limak becomes heavier after `1` year.

Output

```
1
```

---

## Approach

Simulation using a loop.

## Intuition

* Since Limak grows faster than Bob every year, Limak will eventually surpass Bob.
* The simplest and safest approach is to simulate each year’s growth until Limak becomes heavier.

## Algorithm Steps

* Read initial weights `a` and `b`
* Initialize a counter for years
* While `a` is less than or equal to `b`:

  * Multiply `a` by `3`
  * Multiply `b` by `2`
  * Increment year counter
* Output the year count

## Visual Walkthrough

Initial:

```
Limak = a
Bob   = b
```

Each year:

```
Limak = Limak × 3
Bob   = Bob × 2
```

Loop stops when:

```
Limak > Bob
```

## Complexity Analysis

### Time Complexity

O(y)
Where `y` is the number of years required (very small due to fast growth).

### Space Complexity

O(1)
Only a few integer variables are used.

## Solution Explanation

The program simulates the weight changes year by year.
Each iteration represents one year, updating both weights according to the problem rules.

Once Limak’s weight becomes strictly greater than Bob’s, the loop terminates, and the number of iterations gives the required answer.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
using namespace std;

int main() {

    // Initial weights of Limak and Bob
    int a, b;

    // Counter to track number of years
    int year = 0;

    // Read input values
    cin >> a >> b;

    // Continue until Limak becomes strictly heavier than Bob
    while (a <= b) {

        // Limak gains weight by a factor of 3 each year
        a *= 3;

        // Bob gains weight by a factor of 2 each year
        b *= 2;

        // One year has passed
        year++;
    }

    // Output the number of years required
    cout << year << endl;

    return 0;
}
```

## Test Cases Analysis

| a | b | Year-by-Year Growth Ends At | Output |
| - | - | --------------------------- | ------ |
| 4 | 7 | Year 2                      | 2      |
| 1 | 1 | Year 1                      | 1      |
| 2 | 3 | Year 2                      | 2      |
| 5 | 9 | Year 2                      | 2      |

## Edge Cases to Consider

* `a` equals `b` initially
* Very small initial weights
* Minimum valid input values

## Common Test Cases

* Equal starting weights
* Limak significantly lighter than Bob
* Minimal values (`1 1`)

## Common Mistakes to Avoid

* Using `<` instead of `<=` in the loop condition
* Forgetting to increment the year counter
* Misapplying the growth factors

## Interview Relevance

* Tests loop-based simulation
* Reinforces condition-based termination
* Common introductory growth simulation problem

## What This Problem Teaches

* Modeling real-world growth using loops
* Correct loop termination conditions
* Simplicity and correctness over over-optimization

## Key Takeaways

* Simulation is effective when constraints are small
* Clear loop conditions prevent off-by-one errors
* Incremental updates simplify reasoning

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It emphasizes loop control and basic arithmetic simulation, making it ideal for beginners and interview warm-up practice.