# A. Division

## Platform

Codeforces

## Problem Link

[A. Division](https://codeforces.com/problemset/problem/1669/A)

## Problem Statement

Codeforces categorizes participants into different divisions based on their rating.

The divisions are defined as follows:

* **Division 1**: rating ≥ 1900
* **Division 2**: 1600 ≤ rating ≤ 1899
* **Division 3**: 1400 ≤ rating ≤ 1599
* **Division 4**: rating ≤ 1399

For multiple participants, determine the division corresponding to each rating.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* Each of the next `t` lines contains a single integer representing a participant’s rating.

## Output Format

For each test case, print the division name corresponding to the given rating.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ rating ≤ 3000`

## Examples

### Example 1

Input

```
4
1900
1600
1400
800
```

Explanation

* `1900` → Division 1
* `1600` → Division 2
* `1400` → Division 3
* `800`  → Division 4

Output

```
Division 1
Division 2
Division 3
Division 4
```

### Example 2

Input

```
3
2000
1700
1500
```

Explanation
Each rating falls into a different division category.

Output

```
Division 1
Division 2
Division 3
```

## Approach

**Conditional Classification Using Range Checks**

## Intuition

Each rating belongs to exactly one division based on fixed numeric ranges.
By checking the rating from highest to lowest threshold, the correct division can be determined using simple conditional statements.

## Algorithm Steps

* Read the number of test cases
* For each test case:

  * Read the rating
  * Compare it against division thresholds
  * Print the corresponding division name

## Visual Walkthrough

Consider a rating of `1650`:

```
Is rating ≥ 1900? → No
Is rating ≥ 1600? → Yes
```

Result:

```
Division 2
```

Another rating:

```
rating = 1350
```

Falls below all higher thresholds:

```
Division 4
```

## Complexity Analysis

### Time Complexity

O(t)

Each test case is processed once.

### Space Complexity

O(1)

Only constant extra variables are used.

## Solution Explanation

The solution evaluates each rating using a sequence of `if-else` conditions.
By ordering the conditions from highest division to lowest, the correct classification is guaranteed without ambiguity.

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

        // Participant rating
        int rating;
        cin >> rating;

        // Determine division based on rating
        if (rating >= 1900) {
            cout << "Division 1\n";
        }
        else if (rating >= 1600 && rating <= 1899) {
            cout << "Division 2\n";
        }
        else if (rating >= 1400 && rating <= 1599) {
            cout << "Division 3\n";
        }
        else {
            cout << "Division 4\n";
        }
    }

    return 0;
}
```

## Test Cases Analysis

| Rating | Expected Division |
| ------ | ----------------- |
| 1900   | Division 1        |
| 1800   | Division 2        |
| 1500   | Division 3        |
| 1000   | Division 4        |

## Edge Cases to Consider

* Rating exactly on division boundaries
* Very low ratings
* Very high ratings

## Common Test Cases

* Boundary values like `1400`, `1600`, `1900`
* Mixed ratings across all divisions
* Single test case input

## Common Mistakes to Avoid

* Incorrect comparison operators
* Overlapping or missing ranges
* Printing incorrect division labels

## Interview Relevance

* Tests conditional logic
* Evaluates understanding of range-based classification
* Common introductory problem in competitive programming

## What This Problem Teaches

* Proper use of conditional statements
* Importance of ordering conditions correctly
* Translating rules into code accurately

## Key Takeaways

* Always check higher thresholds first
* Ensure ranges are complete and non-overlapping
* Simple logic can produce clean and efficient solutions

## Problem Difficulty Analysis

This is an **Easy-level** problem.
It focuses on basic condition handling and input processing, making it ideal for beginners and interview warm-up exercises.
