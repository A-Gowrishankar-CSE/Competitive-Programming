# B_Blank_Space

## Platform

Codeforces

## Problem Link

[B. Blank Space](https://codeforces.com/problemset/problem/1829/B)

## Problem Statement

You are given multiple test cases.
In each test case, an array consisting only of `0`s and `1`s is provided.

Your task is to determine the **maximum number of consecutive `0`s** (blank spaces) present in the array.

## Input Format

* The first line contains an integer `t`, the number of test cases.
* For each test case:

  * An integer `n`, the size of the array
  * A line containing `n` integers (`0` or `1`)

## Output Format

For each test case, print a single integer — the maximum length of a contiguous segment consisting only of `0`s.

Each result should be printed on a new line.

## Constraints

* `1 ≤ t ≤ 1000`
* `1 ≤ n ≤ 100`
* `array[i] ∈ {0, 1}`

## Examples

### Example 1

Input

```
3
5
1 0 0 1 0
4
0 0 0 0
6
1 1 1 1 1 1
```

Explanation

* Test case 1:

  * Longest sequence of zeros is `0 0` → length `2`
* Test case 2:

  * Entire array is zeros → length `4`
* Test case 3:

  * No zeros present → length `0`

Output

```
2
4
0
```

### Example 2

Input

```
1
8
1 0 1 0 0 0 1 0
```

Explanation

* Longest sequence of zeros is `0 0 0` → length `3`

Output

```
3
```

## Approach (Algorithm Name / Type)

**Single-Pass Maximum Consecutive Count (Sliding Counter Technique)**

This approach scans the array once while tracking the current and maximum lengths of consecutive zeros.

## Intuition

While traversing the array:

* Every time a `0` is encountered, the current blank segment grows.
* Every time a `1` is encountered, the current segment ends and resets.

By continuously updating the maximum observed segment length, the longest blank space can be identified efficiently.

## Algorithm Steps

* Read the number of test cases `t`.
* For each test case:

  * Read array size `n`
  * Initialize two variables:

    * `curr` to track current consecutive zeros
    * `maxi` to store the maximum found so far
  * Traverse the array:

    * If the current value is `0`, increment `curr` and update `maxi`
    * If the value is `1`, reset `curr` to `0`
  * Print `maxi`

## Visual Walkthrough

### Test Case 1

Input:

```
1 0 0 1 0
```

Traversal:

```
1 → curr = 0
0 → curr = 1, maxi = 1
0 → curr = 2, maxi = 2
1 → curr = 0
0 → curr = 1
```

Result:

```
2
```

---

### Test Case 2

Input:

```
0 0 0 0
```

Traversal:

```
0 → curr = 1
0 → curr = 2
0 → curr = 3
0 → curr = 4
```

Result:

```
4
```

---

### Test Case 3

Input:

```
1 1 1
```

Traversal:

```
curr never increases
```

Result:

```
0
```

## Complexity Analysis

### Time Complexity

**O(n)** per test case

Each element is processed exactly once.

### Space Complexity

**O(1)**

Only constant extra variables are used.

## Solution Explanation

The solution maintains a running count of consecutive zeros. Whenever a `1` is encountered, this count is reset since a blank segment cannot span across a `1`.

By updating the maximum length during traversal, the algorithm ensures that the longest blank space is found without requiring additional memory or multiple passes.

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

        // Variable to store the maximum consecutive zeros
        int maxi = 0;

        // Variable to track the current consecutive zero count
        int curr = 0;

        // Traverse the array
        while (n--) {

            int x;
            cin >> x;

            // If current element is 1, reset the current counter
            if (x == 1) {
                curr = 0;
            }
            // If current element is 0, increment counter and update maximum
            else {
                curr++;
                if (curr > maxi) {
                    maxi = curr;
                }
            }
        }

        // Output the maximum blank space
        cout << maxi << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Array             | Longest Zero Segment | Output |
| ----------------- | -------------------- | ------ |
| `1 0 0 1 0`       | `0 0`                | 2      |
| `0 0 0 0`         | `0 0 0 0`            | 4      |
| `1 1 1`           | None                 | 0      |
| `1 0 1 0 0 0 1 0` | `0 0 0`              | 3      |

## Edge Cases to Consider

* Array with no zeros
* Array with all zeros
* Single-element array

## Common Test Cases

* Alternating `0` and `1`
* Long continuous block of zeros
* Multiple small zero segments

## Common Mistakes to Avoid

* Forgetting to reset the counter on `1`
* Updating maximum after reset
* Using additional arrays unnecessarily

## Interview Relevance

* Tests array traversal skills
* Reinforces sliding window / counter concepts
* Common problem pattern in interviews

## What This Problem Teaches

* Efficient single-pass scanning
* Tracking maximums dynamically
* Writing clean state-based logic

## Key Takeaways

* Reset logic is crucial in consecutive-count problems
* One pass is sufficient for maximum segment detection
* Minimal variables can solve many array problems

## Problem Difficulty Analysis

This is a **Medium-level** problem (Codeforces B).

It is conceptually simple but requires careful handling of state during traversal, making it a good step up from basic array problems.