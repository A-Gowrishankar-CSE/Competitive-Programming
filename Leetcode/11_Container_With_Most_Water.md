# Container With Most Water

## Platform
**LeetCode**

## Problem Link
[11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

## Problem Statement
You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `i`th line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the **maximum amount of water** a container can store.

**Note**: You may not slant the container.

## Input Format
- `height`: An array of non-negative integers (2 ≤ height.length ≤ 10⁵)
- Each element represents the height of a vertical line (0 ≤ height[i] ≤ 10⁴)

## Output Format
Return an integer representing the maximum area of water that can be contained.

## Constraints
- 2 ≤ n ≤ 10⁵
- 0 ≤ height[i] ≤ 10⁴

## Example

### Example 1
**Input:** 
```
height = [1,8,6,2,5,4,8,3,7]
```
**Output:** 
```
49
```
**Explanation:** 
- Lines at index 1 (height=8) and index 8 (height=7)
- Width = 8 - 1 = 7
- Height = min(8, 7) = 7
- Area = 7 × 7 = 49

### Example 2
**Input:** 
```
height = [1,1]
```
**Output:** 
```
1
```
**Explanation:** 
- Only two lines available
- Area = min(1, 1) × (1 - 0) = 1

### Example 3
**Input:** 
```
height = [4,3,2,1,4]
```
**Output:** 
```
16
```
**Explanation:**
- Lines at index 0 (height=4) and index 4 (height=4)
- Area = min(4, 4) × (4 - 0) = 4 × 4 = 16

---

## Approach: Two-Pointer (Optimal Solution)

## Intuition
The area formed between two lines is determined by:
```
Area = min(height[left], height[right]) × (right - left)
```

**Key Insight**: 
- Start with the widest container (maximum width)
- Move the pointer at the shorter line inward (greedy choice)
- Why? Moving the taller line inward can only decrease area (width decreases, height can't improve)
- Moving the shorter line might find a taller line, potentially increasing area

## Algorithm
1. **Initialize two pointers**:
   - `left = 0` (start of array)
   - `right = n - 1` (end of array)
   - `max = 0` (track maximum area)

2. **While left < right**:
   - Calculate current area: `height[shorter] × (right - left)`
   - Update maximum area if current is larger
   - Move the pointer at the shorter line:
     - If `height[left] < height[right]`: move `left++`
     - Else: move `right--`

3. **Return maximum area**

## Why This Works (Proof)

**Claim**: We never miss the optimal solution.

**Proof by contradiction**:
- Suppose optimal solution uses lines at indices `i` and `j` where `i < j`
- At some point, our pointers are at positions `left ≤ i` and `right ≥ j`
- If we skip from `(left, right)` to `(left', right')` without checking `(i, j)`:
  - This happens only if we moved the pointer away from the taller line
  - But we always move the pointer at the shorter line
  - So we couldn't have skipped `(i, j)` without checking a configuration that dominates it

**Intuitive explanation**: 
- Moving the taller line inward → guaranteed to get worse (width ↓, height can't ↑)
- Moving the shorter line inward → width ↓, but height might ↑ (worth exploring)

## Complexity Analysis
- **Time Complexity**: O(n) — single pass through the array with two pointers
- **Space Complexity**: O(1) — only using constant extra space

## Visual Example

**Input:** height = [1, 8, 6, 2, 5, 4, 8, 3, 7]

```
Indices:  0  1  2  3  4  5  6  7  8
Heights:  1  8  6  2  5  4  8  3  7
          ↑                       ↑
        left                   right

Step 1: left=0, right=8
- Height: min(1, 7) = 1
- Width: 8 - 0 = 8
- Area: 1 × 8 = 8
- Move left++ (1 < 7, move shorter)

Step 2: left=1, right=8
- Height: min(8, 7) = 7
- Width: 8 - 1 = 7
- Area: 7 × 7 = 49 ← Maximum!
- Move right-- (8 > 7, move shorter)

Step 3: left=1, right=7
- Height: min(8, 3) = 3
- Width: 7 - 1 = 6
- Area: 3 × 6 = 18
- Move right--

... (continue until left >= right)

Final answer: 49
```

## Full Solution

```java
class Solution {
    public int maxArea(int[] height) {
        // Get array length and initialize variables
        int n = height.length;
        int max = 0;          // Maximum area found so far
        int left = 0;         // Left pointer (start)
        int right = n - 1;    // Right pointer (end)
        
        // Two-pointer approach: narrow down from both ends
        while(left < right) {
            int curr = 0;     // Current area
            
            // Calculate area and move pointer at shorter line
            if(height[left] < height[right]) {
                // Left line is shorter
                // Area = height × width
                curr = height[left] * (right - left);
                left++;  // Move left pointer inward
            } else {
                // Right line is shorter or equal
                // Area = height × width
                curr = height[right] * (right - left);
                right--; // Move right pointer inward
            }
            
            // Update maximum area if current is larger
            max = Math.max(max, curr);
        }
        
        return max;
    }
}
```

## Step-by-Step Trace

**Input:** height = [4, 3, 2, 1, 4]

```
Initial: left=0, right=4, max=0

Iteration 1:
- left=0 (h=4), right=4 (h=4)
- min(4, 4) = 4, width = 4
- area = 4 × 4 = 16
- max = 16
- Move right-- (heights equal, arbitrary choice)

Iteration 2:
- left=0 (h=4), right=3 (h=1)
- min(4, 1) = 1, width = 3
- area = 1 × 3 = 3
- max = 16
- Move right-- (1 < 4)

Iteration 3:
- left=0 (h=4), right=2 (h=2)
- min(4, 2) = 2, width = 2
- area = 2 × 2 = 4
- max = 16
- Move right--

Iteration 4:
- left=0 (h=4), right=1 (h=3)
- min(4, 3) = 3, width = 1
- area = 3 × 1 = 3
- max = 16
- Move right--

Loop ends (left >= right)
Return: 16
```

## Key Insights

1. **Greedy Choice**: Always move the pointer at the shorter line — this is the greedy strategy
2. **Width-Height Tradeoff**: As width decreases, we need increasing height to improve area
3. **Optimal Substructure**: Each step eliminates suboptimal solutions
4. **No Backtracking Needed**: Two-pointer approach guarantees we check the optimal pair
5. **Linear Time**: Only one pass needed, unlike O(n²) brute force

## Comparison with Brute Force

### Brute Force Approach (Not Recommended)
```java
public int maxArea(int[] height) {
    int max = 0;
    for(int i = 0; i < height.length; i++) {
        for(int j = i + 1; j < height.length; j++) {
            int area = Math.min(height[i], height[j]) * (j - i);
            max = Math.max(max, area);
        }
    }
    return max;
}
```
- **Time**: O(n²)
- **Space**: O(1)
- **Not optimal** for large inputs

| Aspect | Two-Pointer | Brute Force |
|--------|-------------|-------------|
| **Time** | O(n) ✓ | O(n²) |
| **Space** | O(1) ✓ | O(1) ✓ |
| **Pairs Checked** | ~n | n(n-1)/2 |
| **Optimal** | Yes ✓ | Yes ✓ |

## Edge Cases Handled

1. **Minimum array (n=2)**: [1,1] → 1
2. **All same heights**: [5,5,5,5] → 15 (indices 0 and 3)
3. **Increasing heights**: [1,2,3,4,5] → 6 (indices 0 and 4: min(1,5)×4 = 4, or 1 and 3: 2×3=6)
4. **Decreasing heights**: [5,4,3,2,1] → 6
5. **One very tall line**: [1,1,1,1,100,1] → 4

## Common Mistakes to Avoid

1. **Moving wrong pointer**: Always move the pointer at the shorter line
2. **Width calculation**: Width = `right - left`, not `right - left + 1`
3. **Height calculation**: Use `min(height[left], height[right])`, not max
4. **Off-by-one errors**: Ensure `left < right`, not `left <= right`
5. **Integer overflow**: With constraints (10⁴ × 10⁵), int is sufficient

## Optimization Notes

The given solution can be slightly optimized:
```java
// Slightly more efficient: calculate width once
while(left < right) {
    int width = right - left;
    int h = Math.min(height[left], height[right]);
    max = Math.max(max, h * width);
    
    if(height[left] < height[right]) left++;
    else right--;
}
```

## Practice Tips

1. **Visualize**: Draw the lines and containers
2. **Prove to yourself**: Understand why moving shorter pointer is optimal
3. **Test edge cases**: Two elements, equal heights, extreme values
4. **Explain greedy choice**: Key interview talking point
5. **Compare with brute force**: Show you understand trade-offs

## Follow-Up Questions

1. **Can we use dynamic programming?** → Not beneficial, two-pointer is optimal
2. **What if we can slant the container?** → Different problem, need calculus/geometry
3. **What about 3D containers?** → Extends to max volume with similar greedy approach
4. **Can we parallelize?** → Difficult due to sequential dependency
5. **What if heights can be negative?** → Would need to redefine problem constraints

---

**Note**: This problem is a classic example of the **two-pointer technique** and **greedy algorithms**. The key insight that moving the shorter line is always the right choice demonstrates elegant problem-solving. It's a favorite interview question for testing algorithmic thinking and optimization skills.