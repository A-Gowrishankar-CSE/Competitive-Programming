# 3074. Apple Redistribution into Boxes

## Platform

LeetCode

## Problem Link

[3074. Apple Redistribution into Boxes](https://leetcode.com/problems/apple-redistribution-into-boxes/)

## Problem Statement

You are given two integer arrays:

* `apple` — where each element represents the number of apples in a pile
* `capacity` — where each element represents the maximum number of apples a box can hold

You want to place **all apples from all piles** into some of the boxes.

Each box can be used **at most once**, and apples can be distributed arbitrarily among boxes as long as box capacities are not exceeded.

Your task is to determine the **minimum number of boxes** required to store all the apples.

## Input Format

* An integer array `apple`
* An integer array `capacity`

## Output Format

Return a single integer representing the minimum number of boxes needed.

## Constraints

* `1 ≤ apple.length, capacity.length ≤ 50`
* `1 ≤ apple[i], capacity[i] ≤ 1000`
* It is guaranteed that the total capacity is sufficient to store all apples

## Examples

### Example 1

Input

```
apple = [1, 3, 2]
capacity = [4, 3, 1, 5]
```

Explanation

Total apples:

```
1 + 3 + 2 = 6
```

Using largest boxes first:

```
5 → covers most apples
Remaining apples = 1
```

Second box:

```
+1 capacity → total capacity ≥ 6
```

Output

```
2
```

### Example 2

Input

```
apple = [5, 5, 5]
capacity = [2, 4, 8]
```

Explanation

Total apples:

```
15
```

Sorted capacities:

```
8 + 4 + 2 = 14 (not enough)
```

Add remaining box:

```
All apples fit using 3 boxes
```

Output

```
3
```

## Approach

Greedy strategy using sorting.

## Intuition

To minimize the number of boxes used, we should **always choose the boxes with the largest capacities first**.

By filling the largest boxes before smaller ones, we can cover the total number of apples using the fewest boxes possible.

## Algorithm Steps

* Compute the total number of apples
* Sort the `capacity` array in descending order
* Initialize a cumulative capacity variable
* Iterate through the sorted capacities:

  * Add the current box’s capacity
  * If cumulative capacity ≥ total apples:

    * Return the number of boxes used so far
* Return the result

## Visual Walkthrough

Apples:

```
[2, 4, 1] → total = 7
```

Capacities (sorted descending):

```
[5, 3, 2]
```

Accumulation:

```
5 → not enough
5 + 3 = 8 → sufficient
```

Boxes used:

```
2
```

## Complexity Analysis

### Time Complexity

**O(n log n)**
Sorting the capacity array dominates the runtime.

### Space Complexity

**O(1)** (ignoring input storage)
Only a few integer variables are used.

## Solution Explanation

The solution first calculates the total number of apples that must be stored.

It then sorts the box capacities in descending order so that the largest boxes are used first.
By accumulating capacities one by one, the algorithm stops as soon as the total capacity is sufficient.

This greedy approach is optimal because using larger boxes earlier always minimizes the number of boxes required.

## Full Solution

### C++ Implementation

```cpp
class Solution {
public:
    int minimumBoxes(vector<int>& apple, vector<int>& capacity) {

        // Calculate total number of apples
        int totalApple = 0;
        for (int i : apple)
            totalApple += i;

        // Sort capacities in descending order
        sort(capacity.rbegin(), capacity.rend());

        // Accumulate capacities until enough space is available
        int currentCapacity = 0;
        for (int i = 0; i < capacity.size(); i++) {
            currentCapacity += capacity[i];

            // Once total capacity is sufficient, return box count
            if (currentCapacity >= totalApple)
                return i + 1;
        }

        return 0;
    }
};
```

## Test Cases Analysis

| Apples    | Capacities   | Output |
| --------- | ------------ | ------ |
| [1, 2, 3] | [3, 3, 3]    | 2      |
| [5]       | [5]          | 1      |
| [10, 10]  | [15, 5]      | 2      |
| [2, 2, 2] | [1, 1, 1, 6] | 1      |

## Edge Cases to Consider

* Only one apple pile
* One very large capacity box
* Many small boxes
* Total apples exactly matching cumulative capacity

## Common Test Cases

* Capacities already sorted
* Capacities in random order
* Large apple count with small boxes

## Common Mistakes to Avoid

* Not sorting capacities in descending order
* Summing capacities before apples
* Returning incorrect box count index

## Interview Relevance

* Demonstrates greedy algorithm design
* Tests sorting and accumulation logic
* Common optimization-based interview problem

## What This Problem Teaches

* How greedy choices lead to optimal solutions
* Importance of ordering in resource allocation
* Translating constraints into efficient logic

## Key Takeaways

* Greedy strategies work well when choosing the largest resource first
* Sorting can simplify decision-making
* Always stop early when conditions are satisfied

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on greedy thinking and basic array operations, making it suitable for beginners and interview preparation.