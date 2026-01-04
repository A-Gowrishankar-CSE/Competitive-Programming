# 1390. Four Divisors

## Platform

LeetCode

## Problem Link

[1390. Four Divisors](https://leetcode.com/problems/four-divisors/)

## Problem Statement

You are given an array of integers `nums`.

For each integer `num` in the array:

* If `num` has **exactly four distinct divisors**, add the **sum of those divisors** to the answer.
* Otherwise, add `0`.

Return the total sum over all elements in the array.

## Input Format

* An integer array `nums`

## Output Format

* A single integer representing the sum of divisors for numbers having exactly four divisors

## Constraints

* `1 ≤ nums.length ≤ 10^4`
* `1 ≤ nums[i] ≤ 10^5`

## Examples

### Example 1

Input

```
nums = [21, 4, 7]
```

Explanation

* `21` has divisors `{1, 3, 7, 21}` → exactly 4 divisors → sum = `32`
* `4` has divisors `{1, 2, 4}` → only 3 divisors → ignored
* `7` has divisors `{1, 7}` → only 2 divisors → ignored

Output

```
32
```

### Example 2

Input

```
nums = [8, 10, 3]
```

Explanation

* `8` has divisors `{1, 2, 4, 8}` → exactly 4 divisors → sum = `15`
* `10` has divisors `{1, 2, 5, 10}` → exactly 4 divisors → sum = `18`
* `3` has divisors `{1, 3}` → ignored

Output

```
33
```

## Approach

**Divisor Enumeration up to √n**

## Intuition

A number has exactly **four divisors** only in very specific cases:

* Either it is of the form `p³` where `p` is prime
* Or it is the product of two distinct primes `p × q`

Instead of explicitly checking primality or factorization, the solution efficiently:

* Iterates only up to `√n`
* Counts divisors in pairs
* Accumulates their sum

This avoids unnecessary computations and works efficiently within constraints.

## Algorithm Steps

For each number `n`:

* Initialize `count = 0` and `sum = 0`
* Loop `i` from `1` to `√n`
* If `i` divides `n`:

  * Increment divisor count
  * Add `i` to sum
  * If `i != n / i`, count and add the paired divisor
* After the loop:

  * If `count == 4`, return `sum`
  * Otherwise, return `0`

Repeat this process for all numbers in the array and accumulate the results.

## Visual Walkthrough

Number:

```
n = 10
```

Divisors found:

```
1 and 10
2 and 5
```

Count:

```
4 divisors
```

Sum:

```
1 + 2 + 5 + 10 = 18
```

Included in final answer.

Number:

```
n = 16
```

Divisors:

```
1, 2, 4, 8, 16
```

Count:

```
5 divisors
```

Ignored.

## Complexity Analysis

### Time Complexity

For each number:

```
O(√n)
```

Total:

```
O(m × √n)
```

where `m` is the size of the array.

### Space Complexity

O(1)

Only constant extra space is used.

## Solution Explanation

The helper function `numberOfDivisors` computes the divisor count and sum efficiently by scanning only up to the square root of the number.

Divisors always appear in pairs, which allows both counting and summing to be done correctly without redundancy.

The main function iterates through the array and accumulates the sum only for valid numbers.

## Full Solution

### C++ Implementation

```cpp
class Solution {
public:

    // Helper function to calculate the sum of divisors
    // only if the number has exactly 4 divisors
    int numberOfDivisors(int n) {

        int count = 0;  // To count the number of divisors
        int sum = 0;    // To store the sum of divisors

        // Iterate up to sqrt(n) to find divisor pairs
        for (int i = 1; i * i <= n; i++) {

            // If i divides n
            if (n % i == 0) {

                // Count and add divisor i
                count++;
                sum += i;

                // If i is not the square root,
                // count and add the paired divisor n / i
                if (i != n / i) {
                    count++;
                    sum += n / i;
                }
            }
        }

        // Return sum only if there are exactly 4 divisors
        return count == 4 ? sum : 0;
    }

    // Main function
    int sumFourDivisors(vector<int>& nums) {

        int sum = 0;

        // Process each number in the array
        for (int num : nums) {
            sum += numberOfDivisors(num);
        }

        return sum;
    }
};
```

## Test Cases Analysis

| Number | Divisors    | Count | Included | Sum |
| -----: | ----------- | ----- | -------- | --- |
|     21 | 1, 3, 7, 21 | 4     | Yes      | 32  |
|     10 | 1, 2, 5, 10 | 4     | Yes      | 18  |
|      8 | 1, 2, 4, 8  | 4     | Yes      | 15  |
|      4 | 1, 2, 4     | 3     | No       | 0   |
|      7 | 1, 7        | 2     | No       | 0   |

## Edge Cases to Consider

* Prime numbers
* Perfect squares
* Numbers with more than four divisors

## Common Test Cases

* Products of two primes
* Cubes of primes
* Large composite numbers

## Common Mistakes to Avoid

* Iterating up to `n` instead of `√n`
* Forgetting to count paired divisors
* Miscounting perfect square divisors

## Interview Relevance

* Tests divisor enumeration
* Emphasizes optimization via symmetry
* Common factor-counting problem

## What This Problem Teaches

* Efficient divisor counting
* Pair-based divisor logic
* Avoiding brute-force solutions

## Key Takeaways

* Divisors come in symmetric pairs
* Square root optimization is critical
* Exact divisor count conditions simplify logic

## Problem Difficulty Analysis

This is a **Medium-level** problem.
While the idea is straightforward, it requires careful handling of divisor counting and optimization to pass within constraints.