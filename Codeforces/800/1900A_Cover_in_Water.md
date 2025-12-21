# Cover in Water

## Platform
**Codeforces**

## Problem Link
[A. Cover in Water](https://codeforces.com/problemset/problem/1900/A)

## Problem Statement
You are given a swimming pool represented as a string of length `n` consisting of cells. Each cell is either:
- `.` (dot) - an empty cell that needs to be filled with water
- `#` (hash) - a blocked cell (wall)

You need to fill all empty cells with water. You have two options:
1. Fill any single empty cell using 1 block of water
2. If there are 3 or more consecutive empty cells, you can use an infinite water source that costs only 2 blocks of water to fill all empty cells in the pool

Determine the minimum number of water blocks needed to fill all empty cells.

## Input Format
- The first line contains a single integer `t` (1 ≤ t ≤ 10⁴) — the number of test cases
- For each test case:
  - First line contains integer `n` (1 ≤ n ≤ 100) — the length of the pool
  - Second line contains string `s` of length `n` consisting of characters `.` and `#`

## Output Format
For each test case, print a single integer — the minimum number of water blocks needed to fill all empty cells.

## Constraints
- 1 ≤ t ≤ 10⁴
- 1 ≤ n ≤ 100
- String `s` consists only of `.` and `#`

## Example

### Input
```
5
6
##....
6
.#.#.#
7
...####
8
#..#....
1
#
```

### Output
```
2
3
2
2
0
```

### Explanation
- **Test 1**: `##....` has 4 consecutive dots. Since there are ≥3 consecutive empty cells, we can use infinite water source (cost = 2)
- **Test 2**: `.#.#.#` has 3 separate single empty cells. No 3 consecutive dots, so cost = 3
- **Test 3**: `...####` has 3 consecutive dots at the start. We can use infinite water source (cost = 2)
- **Test 4**: `#..#....` has 2 dots, then 4 consecutive dots. The 4 consecutive dots trigger infinite water (cost = 2)
- **Test 5**: `#` has no empty cells (cost = 0)

## Approach

The solution uses a **greedy approach** with the following logic:

1. **Count total empty cells**: Track the total number of `.` characters
2. **Check for 3+ consecutive empty cells**: If we find 3 or more consecutive empty cells anywhere in the pool, we can use the infinite water source
3. **Optimal decision**:
   - If 3+ consecutive empty cells exist → use infinite water source (cost = 2)
   - Otherwise → fill each empty cell individually (cost = number of dots)

The key insight is that if we have access to infinite water (by having 3+ consecutive empty cells), we only need 2 blocks total regardless of how many empty cells there are.

## Complexity

- **Time Complexity**: O(n) per test case, where n is the length of the string. We traverse the string once.
- **Space Complexity**: O(1) - only using a constant amount of extra space for counters.
- **Overall**: O(t × n) where t is the number of test cases.

## Solution Explanation (Step-by-Step)

1. **Read the number of test cases** `t`
2. **For each test case**:
   - Read the pool length `n` and the pool configuration string `s`
   - Initialize variables:
     - `hasThreeConsecutiveWater` - flag to check if 3+ consecutive dots exist
     - `consecutiveWater` - counter for current consecutive dots
     - `dots` - total count of empty cells
3. **Traverse the string**:
   - If current character is `.`:
     - Increment `consecutiveWater` counter
     - If `consecutiveWater` reaches 3, set the flag to true
     - Increment total `dots` counter
   - If current character is `#`:
     - Reset `consecutiveWater` to 0 (consecutive sequence broken)
4. **Determine the answer**:
   - If `hasThreeConsecutiveWater` is true → output `2`
   - Otherwise → output `dots` (total empty cells)

## Full Solution

```java
import java.util.*;

public class A_Cover_in_Water {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        // Read number of test cases
        int t = sc.nextInt();
        
        while(t-- > 0) {
            // Read pool length and configuration
            int n = sc.nextInt();
            String s = sc.next();
            
            // Flag to check if there are 3+ consecutive empty cells
            boolean hasThreeConsecutiveWater = false;
            
            // Counter for current consecutive empty cells
            int consecutiveWater = 0;
            
            // Total count of empty cells
            int dots = 0;
            
            // Traverse the pool configuration
            for(int i = 0; i < n; i++) {
                if(s.charAt(i) == '.') {
                    // Increment consecutive counter and check if we hit 3
                    if(consecutiveWater++ == 2) {
                        hasThreeConsecutiveWater = true;
                    }
                    dots++; // Count total empty cells
                }
                
                // Reset consecutive counter when we hit a wall
                if(s.charAt(i) == '#') {
                    consecutiveWater = 0;
                }
            }
            
            // Output the minimum water blocks needed
            if(hasThreeConsecutiveWater) {
                // Use infinite water source (costs only 2 blocks)
                System.out.println("2");
            } else {
                // Fill each empty cell individually
                System.out.println(dots);
            }
        }
    }
}
```

---

**Note**: This solution efficiently handles the problem by making a single pass through the string, identifying the optimal strategy based on the presence of 3 or more consecutive empty cells.