# A. Presents

## Platform

Codeforces

## Problem Link

[A. Presents](https://codeforces.com/problemset/problem/136/A)

## Problem Statement

Little Petya very much likes gifts. Recently, he received `n` presents from his friends.

Each friend gives **exactly one present** to exactly **one friend**, and no two friends give a present to the same person.

You are given an array where the `i`-th element denotes the friend to whom the `i`-th friend gave a present.

Your task is to determine, for each friend, **who gave them a present**.

## Input Format

* The first line contains an integer `n`, the number of friends
* The second line contains `n` integers, where the `i`-th integer represents the friend who received a present from friend `i`

## Output Format

Print `n` integers.
The `i`-th integer should represent the friend who gave a present to friend `i`.

## Constraints

* `1 ≤ n ≤ 100`
* `1 ≤ nums[i] ≤ n`
* Each value from `1` to `n` appears exactly once

## Examples

### Example 1

Input

```
4
2 3 4 1
```

Explanation

* Friend 1 gave a present to Friend 2
* Friend 2 gave a present to Friend 3
* Friend 3 gave a present to Friend 4
* Friend 4 gave a present to Friend 1

Reversing this relationship:

* Friend 1 received a present from Friend 4
* Friend 2 received a present from Friend 1
* Friend 3 received a present from Friend 2
* Friend 4 received a present from Friend 3

Output

```
4 1 2 3
```

### Example 2

Input

```
3
1 3 2
```

Explanation

* Friend 1 gave a present to Friend 1
* Friend 2 gave a present to Friend 3
* Friend 3 gave a present to Friend 2

Output

```
1 3 2
```

## Approach

Inverse mapping using an auxiliary array.

## Intuition

The input array represents a **direct mapping**:

```
giver → receiver
```

The problem asks for the **inverse mapping**:

```
receiver → giver
```

By creating a result array and placing the giver index at the receiver’s position, we can reconstruct the required order in a single pass.

## Algorithm Steps

* Read integer `n`
* Read array `nums` of size `n`
* Create a result array `res` of size `n`
* For each index `i`:

  * Place `i + 1` at position `nums[i] - 1` in `res`
* Output the `res` array

## Visual Walkthrough

Input:

```
nums = [2, 3, 4, 1]
```

Mapping process:

```
Friend 1 → Friend 2  → res[1] = 1
Friend 2 → Friend 3  → res[2] = 2
Friend 3 → Friend 4  → res[3] = 3
Friend 4 → Friend 1  → res[0] = 4
```

Final array:

```
res = [4, 1, 2, 3]
```

## Complexity Analysis

### Time Complexity

**O(n)**
Each friend is processed exactly once.

### Space Complexity

**O(n)**
An additional array is used to store the inverse mapping.

## Solution Explanation

The solution builds the inverse of the given permutation.

Since every friend gives exactly one present and every friend receives exactly one present, the input forms a valid permutation.
Using this property, the result array is filled by placing the giver’s index in the position corresponding to the receiver.

This guarantees correctness and simplicity.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of friends
    int n;
    cin >> n;

    // Arrays to store input and result
    int nums[n], res[n];

    // Read input array
    for (int i = 0; i < n; i++)
        cin >> nums[i];

    // Build inverse mapping
    for (int i = 0; i < n; i++) {
        res[nums[i] - 1] = i + 1;
    }

    // Output result
    for (int i : res)
        cout << i << " ";

    return 0;
}
```

## Test Cases Analysis

| n | Input Mapping | Output Mapping |
| - | ------------- | -------------- |
| 1 | 1             | 1              |
| 3 | 1 3 2         | 1 3 2          |
| 4 | 2 3 4 1       | 4 1 2 3        |
| 5 | 5 4 3 2 1     | 5 4 3 2 1      |

## Edge Cases to Consider

* Single friend
* Self-gifting cases
* Completely reversed mappings

## Common Test Cases

* Identity permutation
* Cyclic permutation
* Reverse permutation

## Common Mistakes to Avoid

* Forgetting index offset (`-1` and `+1`)
* Printing the original array instead of the inverse
* Using incorrect array size

## Interview Relevance

* Tests understanding of permutations
* Evaluates array indexing skills
* Common inverse-mapping problem

## What This Problem Teaches

* Working with permutations
* Importance of index transformation
* Efficient one-pass array processing

## Key Takeaways

* Many problems reduce to reversing a mapping
* Pay attention to 1-based vs 0-based indexing
* Simple logic can solve permutation problems efficiently

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on array manipulation and index reasoning, making it ideal for beginners and early interview practice.