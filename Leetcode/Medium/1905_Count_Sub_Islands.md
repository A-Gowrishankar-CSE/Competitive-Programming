# Count Sub Islands

## Platform
**LeetCode**

## Problem Link
[1905. Count Sub Islands](https://leetcode.com/problems/count-sub-islands/)

## Problem Statement
You are given two `m × n` binary matrices `grid1` and `grid2` containing only `0`'s (representing water) and `1`'s (representing land). An island is a group of `1`'s connected 4-directionally (horizontal or vertical). Any cells outside of the grid are considered water cells.

An island in `grid2` is considered a **sub-island** if there exists an island in `grid1` that contains **all** the cells that make up this island in `grid2`.

Return the number of islands in `grid2` that are considered sub-islands of `grid1`.

## Input Format
- `grid1`: A 2D binary matrix of size `m × n`
- `grid2`: A 2D binary matrix of size `m × n`

Both matrices contain only `0`s and `1`s.

## Output Format
Return an integer representing the count of sub-islands in `grid2`.

## Constraints
- `m == grid1.length == grid2.length`
- `n == grid1[i].length == grid2[i].length`
- `1 ≤ m, n ≤ 500`
- `grid1[i][j]` and `grid2[i][j]` are either `0` or `1`

## Examples

### Example 1
**Input:**
```
grid1 = [
  [1,1,1,0,0],
  [0,1,1,1,1],
  [0,0,0,0,0],
  [1,0,0,0,0],
  [1,1,0,1,1]
]

grid2 = [
  [1,1,1,0,0],
  [0,0,1,1,1],
  [0,1,0,0,0],
  [1,0,1,1,0],
  [0,1,0,1,0]
]
```

**Output:**
```
3
```

**Explanation:**
In the picture above, the grid on the left is `grid1` and the grid on the right is `grid2`.

The islands in `grid2` are colored:
- **Red islands**: These are sub-islands (every cell exists in `grid1`)
- **Blue islands**: These are NOT sub-islands (some cells don't exist in `grid1`)

There are 3 sub-islands.

### Example 2
**Input:**
```
grid1 = [
  [1,0,1,0,1],
  [1,1,1,1,1],
  [0,0,0,0,0],
  [1,1,1,1,1],
  [1,0,1,0,1]
]

grid2 = [
  [0,0,0,0,0],
  [1,1,1,1,1],
  [0,1,0,1,0],
  [0,1,0,1,0],
  [1,0,0,0,1]
]
```

**Output:**
```
2
```

**Explanation:**
The island in row 2, columns 1-3 of `grid2` is NOT a sub-island because cell (2,1) is land in `grid2` but water in `grid1`.
The two sub-islands are at rows 1 and 4.

### Example 3
**Input:**
```
grid1 = [
  [1,1],
  [1,1]
]

grid2 = [
  [1,0],
  [0,1]
]
```

**Output:**
```
2
```

**Explanation:**
Both cells in `grid2` that are land also exist as land in `grid1`, forming 2 separate sub-islands.

### Example 4
**Input:**
```
grid1 = [
  [1,1,1],
  [1,1,1],
  [1,1,1]
]

grid2 = [
  [1,1,1],
  [1,1,1],
  [1,1,1]
]
```

**Output:**
```
1
```

**Explanation:**
All of `grid2` forms one island, and it's completely contained in `grid1`.

## Approach
**Two-Pass DFS with Island Elimination**

## Intuition
The key insight is understanding what makes an island in `grid2` a **sub-island**:
- Every land cell of an island in `grid2` must also be land in `grid1` at the same position
- If even one cell of a `grid2` island is water in `grid1`, the entire island is NOT a sub-island

The clever approach is to **eliminate invalid islands first**:
1. **First Pass**: Remove all islands from `grid2` that have at least one cell where `grid1` has water
2. **Second Pass**: Count the remaining islands in `grid2` (these are guaranteed to be sub-islands)

By removing invalid islands in the first pass, we ensure that any island remaining in `grid2` must be a complete sub-island of `grid1`.

## Algorithm Steps

### Phase 1: Eliminate Invalid Islands
1. Iterate through every cell `(i, j)` in both grids
2. If `grid1[i][j] == 0` (water) AND `grid2[i][j] == 1` (land):
   - This cell in `grid2` cannot be part of a sub-island
   - Use DFS to remove the entire island containing this cell from `grid2`
3. After this phase, only potential sub-islands remain in `grid2`

### Phase 2: Count Remaining Islands
1. Iterate through every cell `(i, j)` in `grid2`
2. If `grid2[i][j] == 1`:
   - This is the start of a sub-island
   - Use DFS to mark the entire island as visited (set to 0)
   - Increment counter
3. Return the counter

### DFS Helper Function
- **Purpose**: Marks all connected land cells as visited (sets to 0)
- **Base Case**: Return if out of bounds or current cell is water (0)
- **Process**: Mark current cell as 0, then recursively visit all 4 neighbors

## Visual Walkthrough

Let's trace Example 1 with a simplified version:

**Initial State:**
```
grid1:          grid2:
[1,1,0]         [1,1,0]
[0,1,1]         [0,0,1]
[1,0,0]         [1,1,0]
```

**Phase 1: Eliminate Invalid Islands**

Check position (1,2): `grid1[1][2] = 1`, `grid2[1][2] = 1` ✓ Valid
Check position (2,1): `grid1[2][1] = 0`, `grid2[2][1] = 1` ✗ Invalid!

Remove island containing (2,1) from grid2:
```
grid2 after Phase 1:
[1,1,0]
[0,0,1]
[0,0,0]  ← Island eliminated
```

**Phase 2: Count Remaining Islands**

Island 1: Starting at (0,0)
```
[X,X,0]  ← Mark as visited
[0,0,1]
[0,0,0]
Count = 1
```

Island 2: Starting at (1,2)
```
[0,0,0]
[0,0,X]  ← Mark as visited
[0,0,0]
Count = 2
```

**Result:** 2 sub-islands

## Complexity Analysis

### Time Complexity
**O(m × n)** where:
- `m` is the number of rows
- `n` is the number of columns

**Reasoning:**
- **Phase 1**: We iterate through all `m × n` cells once: O(m × n)
  - Each cell is visited at most once during DFS (marked as 0)
- **Phase 2**: We iterate through all `m × n` cells again: O(m × n)
  - Again, each cell visited at most once during DFS
- **Total**: O(m × n) + O(m × n) = O(m × n)

Even though we have nested loops and recursive DFS calls, each cell is processed at most twice (once in each phase), making it linear in the number of cells.

### Space Complexity
**O(m × n)** where:
- `m` is the number of rows
- `n` is the number of columns

**Reasoning:**
- **Recursion Stack**: In the worst case (all cells form one snake-like island), DFS recursion depth can be O(m × n)
- **In-place Modification**: We modify `grid2` directly, so no additional space for visited array
- **No Extra Data Structures**: Only using a simple counter variable

**Note**: If grid modification is not allowed, we'd need an O(m × n) visited array.

## Solution Explanation

The solution uses a **two-phase elimination strategy**:

### Phase 1: Invalid Island Removal
The brilliant insight is to identify and remove "disqualified" islands early:
- If any part of a `grid2` island overlaps with water in `grid1`, the entire island is invalid
- We scan for cells where `grid1[i][j] == 0` and `grid2[i][j] == 1`
- When found, we use DFS to erase the entire island from `grid2`
- This ensures that after Phase 1, only valid candidates remain

### Phase 2: Sub-Island Counting
After removing invalid islands:
- Any remaining island in `grid2` is guaranteed to be a sub-island
- We simply count islands using standard DFS traversal
- Each discovered island increments our counter

### Why This Works
By eliminating invalid islands first, we transform a complex "validation while counting" problem into a simple "count remaining islands" problem. This separation of concerns makes the solution elegant and efficient.

**Key Observations:**
1. If a `grid2` island has even one cell that's water in `grid1`, it's not a sub-island
2. After removing all such islands, everything left must be valid
3. We don't need to track which island each cell belongs to—just mark and count

## Full Solution

### Java Implementation
```java
class Solution {
    // Helper DFS function to mark all connected land cells as visited
    public static void dfs(int[][] grid, int row, int col) {
        // Base case: out of bounds or water
        if(row < 0 || col < 0 || row > grid.length - 1 || 
           col > grid[0].length - 1 || grid[row][col] == 0) {
            return;
        }
        
        // Mark current cell as visited (set to water)
        grid[row][col] = 0;
        
        // Recursively visit all 4 adjacent cells
        dfs(grid, row - 1, col);  // up
        dfs(grid, row, col + 1);  // right
        dfs(grid, row + 1, col);  // down
        dfs(grid, row, col - 1);  // left
    }
    
    public int countSubIslands(int[][] grid1, int[][] grid2) {
        // Phase 1: Eliminate invalid islands from grid2
        // Remove any island in grid2 that has cells where grid1 is water
        for(int i = 0; i < grid1.length; i++) {
            for(int j = 0; j < grid1[0].length; j++) {
                // If grid1 has water but grid2 has land
                if(grid1[i][j] == 0 && grid2[i][j] == 1) {
                    // Remove entire island from grid2 using DFS
                    dfs(grid2, i, j);
                }
            }
        }
        
        // Phase 2: Count remaining islands in grid2
        // All remaining islands are guaranteed to be sub-islands
        int count = 0;
        for(int i = 0; i < grid1.length; i++) {
            for(int j = 0; j < grid1[0].length; j++) {
                // If we find unvisited land in grid2
                if(grid2[i][j] == 1) {
                    // Mark entire island as visited and increment counter
                    dfs(grid2, i, j);
                    count++;
                }
            }
        }
        
        return count;
    }
}
```

### C++ Implementation
```cpp
class Solution {
public:
    // Helper DFS function to mark all connected land cells as visited
    void dfs(vector<vector<int>>& grid, int row, int col) {
        // Base case: out of bounds or water
        if(row < 0 || col < 0 || row > grid.size() - 1 || 
           col > grid[0].size() - 1 || grid[row][col] == 0) {
            return;
        }
        
        // Mark current cell as visited (set to water)
        grid[row][col] = 0;
        
        // Recursively visit all 4 adjacent cells
        dfs(grid, row - 1, col);  // up
        dfs(grid, row, col + 1);  // right
        dfs(grid, row + 1, col);  // down
        dfs(grid, row, col - 1);  // left
    }
    
    int countSubIslands(vector<vector<int>>& grid1, vector<vector<int>>& grid2) {
        // Phase 1: Eliminate invalid islands from grid2
        // Remove any island in grid2 that has cells where grid1 is water
        for(int i = 0; i < grid1.size(); i++) {
            for(int j = 0; j < grid1[0].size(); j++) {
                // If grid1 has water but grid2 has land
                if(grid1[i][j] == 0 && grid2[i][j] == 1) {
                    // Remove entire island from grid2 using DFS
                    dfs(grid2, i, j);
                }
            }
        }
        
        // Phase 2: Count remaining islands in grid2
        // All remaining islands are guaranteed to be sub-islands
        int count = 0;
        for(int i = 0; i < grid1.size(); i++) {
            for(int j = 0; j < grid1[0].size(); j++) {
                // If we find unvisited land in grid2
                if(grid2[i][j] == 1) {
                    // Mark entire island as visited and increment counter
                    dfs(grid2, i, j);
                    count++;
                }
            }
        }
        
        return count;
    }
};
```

## Test Cases Analysis

| Grid1 | Grid2 | Invalid Islands Removed | Valid Islands | Output | Notes |
|-------|-------|------------------------|---------------|--------|-------|
| `[[1,1],[1,1]]` | `[[1,1],[1,1]]` | None | 1 | 1 | Complete overlap |
| `[[1,0],[0,1]]` | `[[1,1],[1,1]]` | 1 (all of grid2) | 0 | 0 | No valid sub-island |
| `[[1,1],[1,1]]` | `[[1,0],[0,1]]` | None | 2 | 2 | Two separate valid islands |
| `[[0,0],[0,0]]` | `[[1,1],[1,1]]` | 1 (all of grid2) | 0 | 0 | Grid1 all water |
| `[[1,1],[1,1]]` | `[[0,0],[0,0]]` | None | 0 | 0 | Grid2 all water |
| `[[1,1,1],[1,0,1],[1,1,1]]` | `[[0,1,0],[1,1,1],[0,1,0]]` | None | 1 | 1 | Cross pattern |
| `[[1,0,1],[0,1,0],[1,0,1]]` | `[[1,1,1],[1,1,1],[1,1,1]]` | 1 (center overlaps) | 4 | 4 | Four corners valid |

## Edge Cases to Consider

1. **Identical Grids**: When `grid1 == grid2`, result should be the count of all islands in grid1
2. **No Overlap**: Grid2 has land where grid1 is all water → result is 0
3. **Complete Inclusion**: All of grid2 is land and contained in grid1's single island → result is 1
4. **Disjoint Islands**: Multiple separate islands in grid2, some valid, some not
5. **Single Cell Islands**: Islands consisting of only one cell
6. **Grid2 Empty**: All water in grid2 → result is 0
7. **Grid1 Empty**: All water in grid1 → result is 0 (no sub-islands possible)
8. **Maximum Size**: 500×500 grids to test performance
9. **Partial Overlap**: Island in grid2 partially overlaps with grid1 island
10. **Adjacent Invalid Cells**: Multiple cells of same island in grid2 are water in grid1

## Common Test Cases

1. **All Valid**: Every island in grid2 is a sub-island of grid1
2. **None Valid**: No island in grid2 qualifies as a sub-island
3. **Mixed Validity**: Some islands valid, others invalid
4. **Border Islands**: Islands touching grid boundaries
5. **Single Large Island**: One large island spanning most of the grid
6. **Many Small Islands**: Grid2 has many 1-cell islands
7. **Snake Pattern**: Long winding island to test DFS depth

## Common Mistakes to Avoid

1. **Single-Pass Validation**: Trying to validate each island during counting leads to complex logic and potential bugs—the two-phase approach is cleaner and more reliable
2. **Forgetting to Mark Visited**: Not setting cells to 0 during DFS causes infinite recursion and incorrect counts
3. **Wrong Invalidation Logic**: Using `grid1[i][j] == 1 && grid2[i][j] == 0` instead of `grid1[i][j] == 0 && grid2[i][j] == 1` completely reverses the solution logic

## Interview Relevance

1. **Two-Grid Problems**: Tests ability to work with multiple related data structures simultaneously—a common pattern in interviews
2. **Problem Transformation**: Demonstrates problem-solving skill by converting complex validation into simple elimination + counting
3. **DFS Mastery**: Requires solid understanding of DFS for both removal and counting operations

## What This Problem Teaches

- **Problem decomposition**: Breaking complex problems into simpler phases
- **Elimination strategy**: Sometimes removing invalid cases is easier than validating valid ones
- **Multi-grid coordination**: Working with corresponding positions in multiple grids
- **DFS applications**: Using DFS for both marking/removal and counting
- **State modification**: Efficiently using in-place modification to track visited cells
- **Invariant maintenance**: Ensuring grid2 only contains valid candidates before counting

## Key Takeaways

- **Two-phase approach** simplifies complex validation problems
- **Early elimination** of invalid cases makes subsequent logic trivial
- **DFS is versatile**: Can be used for removal, counting, validation, etc.
- **Grid correspondence**: When working with multiple grids, align position checks carefully
- **In-place modification** saves space but requires careful phase separation
- **Sub-island definition**: A grid2 island is a sub-island only if ALL its cells are land in grid1
- **Phase separation** prevents mixing of concerns and reduces bugs

## Problem Difficulty Analysis

**Difficulty Level**: Medium

**Skills Required**:
- Depth-First Search (DFS)
- Multi-grid traversal
- Graph connected components
- Problem transformation
- Recursion
- Binary matrix operations

**Why It's Medium Difficulty**:
- Requires understanding of sub-island definition
- Needs clever insight to use two-phase approach
- Must coordinate two grids simultaneously
- Potential for logical errors in validation
- Not immediately obvious why elimination works

**Comparison to Related Problems**:
- Harder than "Number of Islands" (needs two grids)
- Similar to "Number of Distinct Islands" (needs validation)
- Easier than "Number of Islands II" (no dynamic updates)

**Related LeetCode Problems**:
- 200. Number of Islands
- 695. Max Area of Island
- 1254. Number of Closed Islands
- 1905. Count Sub Islands (this problem)
- 827. Making A Large Island

**Time to Solve**: 
- Beginners: 45-60 minutes
- Intermediate: 25-35 minutes
- Advanced: 15-20 minutes

**Interview Tips**:
1. Clarify the sub-island definition with examples
2. Explain the two-phase strategy before coding
3. Walk through why elimination works
4. Mention space-time tradeoffs of in-place modification
5. Consider alternative approaches (single-pass with boolean tracking)
6. Discuss how to avoid modifying input if required
7. Explain DFS vs BFS choice (both work, DFS is more concise)