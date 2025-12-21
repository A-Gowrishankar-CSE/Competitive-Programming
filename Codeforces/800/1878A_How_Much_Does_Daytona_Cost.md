# How Much Does Daytona Cost?

## Platform
**Codeforces**

## Problem Link
[A. How Much Does Daytona Cost?](https://codeforces.com/problemset/problem/1878/A)

## Problem Statement
You are given an array `a` of length `n` and an integer `k`. 

A subarray is considered **good** if the most frequent element in that subarray equals `k`. If there are multiple elements with the same maximum frequency, any of them can equal `k` for the subarray to be good.

Your task is to determine whether there exists at least one good subarray in the given array.

## Input Format
- The first line contains a single integer `t` (1 ≤ t ≤ 1000) — the number of test cases
- For each test case:
  - First line contains two integers `n` and `k` (1 ≤ n ≤ 100, 1 ≤ k ≤ 100) — the length of the array and the target value
  - Second line contains `n` integers `a₁, a₂, ..., aₙ` (1 ≤ aᵢ ≤ 100) — the elements of the array

## Output Format
For each test case, print:
- `"YES"` if there exists at least one good subarray
- `"NO"` otherwise

## Constraints
- 1 ≤ t ≤ 1000
- 1 ≤ n ≤ 100
- 1 ≤ k ≤ 100
- 1 ≤ aᵢ ≤ 100

## Example

### Input
```
4
5 3
1 2 3 4 5
5 5
1 2 3 4 5
4 1
2 3 4 4
3 2
1 1 1
```

### Output
```
YES
YES
NO
NO
```

### Explanation
- **Test 1**: Array = [1, 2, 3, 4, 5], k = 3
  - Subarray [3] contains only element 3, which is the most frequent (appears once). Since 3 = k, this is a good subarray.
  - Answer: `YES`

- **Test 2**: Array = [1, 2, 3, 4, 5], k = 5
  - Subarray [5] contains only element 5, which is the most frequent. Since 5 = k, this is a good subarray.
  - Answer: `YES`

- **Test 3**: Array = [2, 3, 4, 4], k = 1
  - Element 1 doesn't exist in the array, so no subarray can have 1 as its most frequent element.
  - Answer: `NO`

- **Test 4**: Array = [1, 1, 1], k = 2
  - Element 2 doesn't exist in the array. All subarrays have 1 as the most frequent element.
  - Answer: `NO`

## Approach

The solution uses a **simple observation** based on the problem's constraint:

**Key Insight**: If the element `k` exists anywhere in the array, then we can always find a good subarray — specifically, a subarray of length 1 containing only that element `k`.

**Why does this work?**
- A subarray of length 1 contains only one element
- That single element is trivially the most frequent element (frequency = 1)
- If that element equals `k`, then the subarray is good

Therefore, the problem reduces to: **Does the element `k` exist in the array?**

**Algorithm**:
1. Read the array and the value `k`
2. Check if `k` exists in the array
3. If yes → print "YES"
4. If no → print "NO"

## Complexity

- **Time Complexity**: O(n) per test case — traversing the array once to find `k`
- **Space Complexity**: O(n) — storing the array
- **Overall**: O(t × n) where t is the number of test cases

## Solution Explanation (Step-by-Step)

1. **Read the number of test cases** `t`
2. **For each test case**:
   - Read `n` (array length) and `k` (target value)
   - Read the array of `n` integers into `nums`
   - Initialize a counter `count` to 0
   - **Search for k in the array**:
     - Iterate through each element in the array
     - If any element equals `k`:
       - Increment `count`
       - Break the loop (we only need to find one occurrence)
   - **Determine the answer**:
     - If `count > 0` (k was found) → print "YES"
     - Otherwise → print "NO"
3. **Close the scanner** to prevent resource leaks

## Full Solution

```java
import java.util.*;

public class A_How_Much_Does_Daytona_Cost {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        // Read number of test cases
        int t = sc.nextInt();
        
        while (t-- > 0) {
            // Read array length and target value
            int n = sc.nextInt();
            int k = sc.nextInt();
            
            // Read the array
            int[] nums = new int[n];
            for(int i = 0; i < n; i++) {
                nums[i] = sc.nextInt();
            }
            
            // Check if k exists in the array
            int count = 0;
            for(int num : nums) {
                if(num == k) {
                    count++;
                    break; // Found k, no need to continue searching
                }
            }
            
            // If k exists, answer is YES; otherwise NO
            System.out.println(count > 0 ? "YES" : "NO");
        }
        
        // Close scanner to prevent resource leak
        sc.close();
    }
}
```

## Alternative Optimized Approach

The solution can be slightly optimized by using a boolean flag instead of a counter:

```java
boolean found = false;
for(int num : nums) {
    if(num == k) {
        found = true;
        break;
    }
}
System.out.println(found ? "YES" : "NO");
```

## Key Insights

1. **Problem Simplification**: The complex definition of "good subarray" simplifies to checking existence
2. **Single Element Subarrays**: Always consider edge cases like subarrays of length 1
3. **Early Termination**: Once we find `k`, we can immediately return "YES" without checking remaining elements
4. **Boolean Logic**: The problem is essentially a membership test: is `k` ∈ array?

---

**Note**: This problem demonstrates how seemingly complex problems can often be reduced to simple observations. The key is understanding that a single-element subarray containing `k` is always valid if `k` exists in the array.