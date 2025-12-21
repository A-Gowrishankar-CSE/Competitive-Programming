# Roof Construction

## Platform
**Codeforces**

## Problem Link
[B. Roof Construction](https://codeforces.com/problemset/problem/1632/B)

## Problem Statement
You are given an integer `n`. You need to construct a permutation of integers from 0 to n-1 such that the **maximum bitwise XOR** of any two adjacent elements is **minimized**.

More formally, find a permutation `p₀, p₁, ..., pₙ₋₁` of integers [0, 1, 2, ..., n-1] that minimizes:
```
max(p₀ ⊕ p₁, p₁ ⊕ p₂, ..., pₙ₋₂ ⊕ pₙ₋₁)
```

where `⊕` denotes the bitwise XOR operation.

## Input Format
- The first line contains a single integer `t` (1 ≤ t ≤ 10⁴) — the number of test cases
- For each test case:
  - A single line contains integer `n` (2 ≤ n ≤ 2 × 10⁵) — the size of the permutation

## Output Format
For each test case, print `n` space-separated integers — any valid permutation that minimizes the maximum XOR of adjacent elements.

## Constraints
- 1 ≤ t ≤ 10⁴
- 2 ≤ n ≤ 2 × 10⁵
- Sum of n over all test cases ≤ 2 × 10⁵

## Example

### Input
```
3
2
3
4
```

### Output
```
1 0
1 0 2
2 3 1 0
```

### Explanation

**Test 1**: n=2, permutation=[1, 0]
- XOR: 1 ⊕ 0 = 1
- Maximum XOR = 1
- This is optimal (any permutation of [0,1] gives max XOR of 1)

**Test 2**: n=3, permutation=[1, 0, 2]
- XOR: 1 ⊕ 0 = 1, 0 ⊕ 2 = 2
- Maximum XOR = 2
- Optimal (cannot do better than 2)

**Test 3**: n=4, permutation=[2, 3, 1, 0]
- XOR: 2 ⊕ 3 = 1, 3 ⊕ 1 = 2, 1 ⊕ 0 = 1
- Maximum XOR = 2
- Optimal for n=4

## Approach: Bit Manipulation with MSB Analysis

## Intuition

**Key Observation**: The maximum XOR between two numbers is determined by their most significant differing bit (MSB).

**Strategy**:
1. Find the highest power of 2 less than or equal to n-1 (this is the MSB position)
2. Split numbers into two groups:
   - Group 1: Numbers less than this power of 2
   - Group 2: Numbers greater than or equal to this power of 2
3. Arrange Group 1 in descending order, then Group 2 in ascending order
4. This ensures the maximum XOR is minimized at the boundary between groups

**Why this works**:
- Within each group, the MSB is the same, so XOR values are smaller
- At the boundary, we transition smoothly by placing numbers close in value

## Algorithm

1. **Calculate MSB position**:
   - For value (n-1), find the position of the highest set bit
   - Formula: `msb = floor(log₂(n-1))`

2. **Find the split point**:
   - `a = 2^msb` (first power of 2 at or above the MSB position)

3. **Construct permutation**:
   - Print numbers from (a-1) down to 0 (descending)
   - Print numbers from a to (n-1) (ascending)

## Complexity Analysis

- **Time Complexity**: O(n) per test case — printing n numbers
- **Space Complexity**: O(1) — no extra space needed beyond output
- **Overall**: O(sum of all n values)

## Visual Example

**Example**: n = 8

```
Step 1: Find MSB of (n-1) = 7
- 7 in binary: 111
- MSB position: 2 (0-indexed from right)
- 2² = 4

Step 2: Split at a = 4
- Group 1: [0, 1, 2, 3] → print as [3, 2, 1, 0]
- Group 2: [4, 5, 6, 7] → print as [4, 5, 6, 7]

Step 3: Output
[3, 2, 1, 0, 4, 5, 6, 7]

Verify XOR values:
- 3 ⊕ 2 = 1 (011 ⊕ 010 = 001)
- 2 ⊕ 1 = 3 (010 ⊕ 001 = 011)
- 1 ⊕ 0 = 1 (001 ⊕ 000 = 001)
- 0 ⊕ 4 = 4 (000 ⊕ 100 = 100) ← Critical boundary
- 4 ⊕ 5 = 1 (100 ⊕ 101 = 001)
- 5 ⊕ 6 = 3 (101 ⊕ 110 = 011)
- 6 ⊕ 7 = 1 (110 ⊕ 111 = 001)

Maximum XOR = 4 (at boundary)
```

## Binary Analysis

**Why descending then ascending?**

Consider n = 8, split at 4:
```
Binary representations:
0: 000    4: 100
1: 001    5: 101
2: 010    6: 110
3: 011    7: 111

Group 1 (reversed): 3, 2, 1, 0
- Smooth descent in binary values
- Small XOR differences

Boundary: 0 ⊕ 4
- 000 ⊕ 100 = 100 (only MSB differs)
- This is the minimum possible at the boundary

Group 2 (ascending): 4, 5, 6, 7
- Smooth ascent in binary values
- Small XOR differences
```

## Full Solution

```java
import java.util.*;

public class B_Roof_Construction {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        // Read number of test cases
        int t = sc.nextInt();
        
        while (t-- > 0) {
            // Read n (size of permutation: 0 to n-1)
            int n = sc.nextInt();
            n--;  // Work with n-1 as the maximum value
            
            // Find the position of the most significant bit (MSB) of n
            // This determines where to split the permutation
            int msb = (int) (Math.log(n) / Math.log(2));
            
            // Calculate the split point: first power of 2 at MSB position
            int a = (int) Math.pow(2, msb);
            
            // First part: print numbers from (a-1) down to 0 (descending)
            // These are numbers with MSB = 0 at the critical position
            for(int i = a - 1; i >= 0; i--) {
                System.out.print(i + " ");
            }
            
            // Second part: print numbers from a to n (ascending)
            // These are numbers with MSB = 1 at the critical position
            for(int i = a; i <= n; i++) {
                System.out.print(i + " ");
            }
            
            System.out.println();
        }
        
        // Close scanner
        sc.close();
    }
}
```

## Step-by-Step Trace

**Input**: n = 5

```
Step 1: Adjust n
- n = 5 - 1 = 4

Step 2: Find MSB of 4
- 4 in binary: 100
- msb = log₂(4) = 2
- a = 2² = 4

Step 3: Generate permutation
- Part 1: i from (4-1=3) down to 0
  Output: 3 2 1 0
  
- Part 2: i from 4 to 4
  Output: 4

Final output: 3 2 1 0 4

Verification:
- 3 ⊕ 2 = 1
- 2 ⊕ 1 = 3
- 1 ⊕ 0 = 1
- 0 ⊕ 4 = 4 ← Maximum
- Max XOR = 4 (optimal for n=5)
```

## Detailed Example with Binary

**n = 6**

```
Original range: [0, 1, 2, 3, 4, 5]

Binary:
0: 000
1: 001
2: 010
3: 011
4: 100
5: 101

n-1 = 5 (binary: 101)
msb = 2
a = 2² = 4

Permutation: [3, 2, 1, 0, 4, 5]

Binary permutation:
3: 011
2: 010  → XOR = 001 (1)
1: 001  → XOR = 011 (3)
0: 000  → XOR = 001 (1)
4: 100  → XOR = 100 (4) ← Max
5: 101  → XOR = 001 (1)

Maximum XOR = 4
```

## Key Insights

1. **MSB Determines Maximum**: The highest differing bit determines XOR magnitude
2. **Group by MSB**: Numbers with same MSB pattern have smaller XORs
3. **Smooth Transitions**: Descending then ascending minimizes boundary XOR
4. **Power of 2 Split**: Split at 2^msb creates optimal groups
5. **Logarithmic Calculation**: MSB found using log₂

## Why This Is Optimal

**Proof Sketch**:
- The maximum XOR must involve the MSB of (n-1)
- By grouping numbers by their MSB, we ensure internal XORs are smaller
- The boundary XOR is minimized by placing consecutive values (a-1 and a)
- Any other arrangement would have larger XOR somewhere

**Minimum Possible Max XOR**:
For n values [0, n-1], the minimum possible maximum XOR is 2^⌊log₂(n-1)⌋

## Edge Cases

1. **n = 2**: Output [1, 0] → XOR = 1
2. **n = power of 2**: e.g., n=4 → [1, 0, 2, 3]
3. **n = power of 2 + 1**: e.g., n=5 → [3, 2, 1, 0, 4]
4. **Large n**: Algorithm handles up to 2×10⁵ efficiently

## Common Mistakes to Avoid

1. **Forgetting n--**: We work with [0, n-1], not [0, n]
2. **Wrong MSB calculation**: Use log₂ correctly
3. **Off-by-one in loops**: Ensure ranges are [a-1, 0] and [a, n]
4. **Integer overflow**: Math.pow returns double, cast to int
5. **Not closing scanner**: Always close to prevent resource leaks

## Alternative Approaches

### Approach 2: Bit Manipulation
```java
int msb = 31 - Integer.numberOfLeadingZeros(n);
int a = 1 << msb;  // Bit shift instead of Math.pow
```
This is more efficient and avoids floating-point operations.

## Practice Tips

1. **Understand XOR**: Review bitwise XOR properties
2. **Visualize binary**: Draw binary representations
3. **Test small cases**: n=2, 3, 4 by hand
4. **Explain MSB logic**: Key interview talking point
5. **Compare outputs**: Multiple valid answers exist

## Follow-Up Questions

1. **Can there be multiple optimal solutions?** → Yes, many permutations achieve the same max XOR
2. **What if we want to maximize instead?** → Place 0 next to n-1
3. **Can we use bit manipulation?** → Yes, more efficient than Math.log
4. **What's the minimum possible max XOR?** → 2^⌊log₂(n-1)⌋
5. **Does order within groups matter?** → No, as long as transition is smooth

---

**Note**: This problem demonstrates advanced bit manipulation and greedy algorithm design. The key insight is recognizing that the MSB determines XOR magnitude, and grouping by MSB minimizes the maximum XOR. It's a great problem for understanding bitwise operations and optimization strategies.