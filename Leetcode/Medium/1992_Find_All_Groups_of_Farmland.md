# Find All Groups of Farmland

## Platform
**LeetCode**

## Problem Link
[1992. Find All Groups of Farmland](https://leetcode.com/problems/find-all-groups-of-farmland/)

## Problem Statement
You are given a 2D binary matrix `land` of size `m × n` representing a farm. The matrix contains only `0`s (representing forested land) and `1`s (representing farmland).

Groups of farmland are formed by connecting adjacent cells horizontally or vertically that contain `1`s. Each group of farmland is a **rectangular** shaped group (guaranteed by the problem constraints).

For each group of farmland, you need to find its top-left corner `(r1, c1)` and bottom-right corner `(r2, c2)`.

Return a 2D array containing the coordinates of all groups of farmland. Each element should be in the format `[r1, c1, r2, c2]` where:
- `(r1, c1)` is the coordinate of the top-left cell of the farmland group
- `(r2, c2)` is the coordinate of the bottom-right cell of the farmland group

The answer can be returned in any order.

## Input Format
- `land`: A 2D binary matrix of size `m × n` where:
  - `land[i][j] == 1` represents farmland
  - `land[i][j] == 0` represents forest

## Output Format
Return a 2D integer array where each row contains `[r1, c1, r2, c2]` representing one farmland group.

## Constraints
- `m == land.length`
- `n == land[i].length`
- `1 ≤ m, n ≤ 300`
- `land` consists of only `0`s and `1`s
- Groups of farmland are **rectangular** in shape (guaranteed)

## Examples

### Example 1
**Input:**
```
land = [
  [1,0,0],
  [0,1,1],
  [0,1,1]
]
```

**Output:**
```
[[0,0,0,0],[1,1,2,2]]
```

**Explanation:**
- First farmland group: Single cell at position (0,0), so top-left is (0,0) and bottom-right is also (0,0)
- Second farmland group: 2×2 rectangle from (1,1) to (2,2)
  ```
  [1,1] [1,2]
  [2,1] [2,2]
  ```

### Example 2
**Input:**
```
land = [
  [1,1],
  [1,1]
]
```

**Output:**
```
[[0,0,1,1]]
```

**Explanation:**
- The entire grid forms one 2×2 farmland group
- Top-left corner: (0,0)
- Bottom-right corner: (1,1)

### Example 3
**Input:**
```
land = [
  [0]
]
```

**Output:**
```
[]
```

**Explanation:**
- No farmland present, return empty array

### Example 4
**Input:**
```
land = [
  [1,1,1],
  [1,1,1],
  [1,1,1]
]
```

**Output:**
```
[[0,0,2,2]]
```

**Explanation:**
- Entire 3×3 grid is one farmland group
- Top-left: (0,0), Bottom-right: (2,2)

### Example 5
**Input:**
```
land = [
  [1,0,1],
  [0,0,0],
  [1,0,1]
]
```

**Output:**
```
[[0,0,0,0],[0,2,0,2],[2,0,2,0],[2,2,2,2]]
```

**Explanation:**
- Four separate 1×1 farmland groups at the four corners
- Each cell forms its own group where top-left = bottom-right

## Approach
**Depth-First Search (DFS) with Boundary Tracking**

## Intuition
The problem guarantees that all farmland groups are **rectangular**. This is a crucial constraint that simplifies our solution significantly.

Key insights:
1. Since farmlands are rectangular, we only need to find two corners: top-left and bottom-right
2. The top-left corner is where we start our DFS (the first `1` we encounter)
3. During DFS traversal, we track the maximum row and column reached—this gives us the bottom-right corner
4. We mark visited cells as `0` to avoid processing them again

The algorithm:
- Scan the grid left-to-right, top-to-bottom
- When we find an unvisited farmland cell (`1`), it's the top-left corner
- Use DFS to explore the entire rectangular farmland
- Track the maximum row and column during DFS—this is the bottom-right corner
- Mark all visited cells as `0` to prevent reprocessing

## Algorithm Steps

1. **Initialize Result List**: Create a list to store farmland coordinates
2. **Traverse Grid**: Iterate through each cell `(i, j)` in the land matrix
3. **Detect Farmland Start**:
   - If `land[i][j] == 1`, we found the top-left corner of a farmland group
   - Initialize `maxRow = i` and `maxCol = j`
4. **Explore Farmland via DFS**:
   - Call `dfs(land, i, j)` to traverse the entire farmland
   - During traversal, update `maxRow` and `maxCol` to track boundaries
   - Mark visited cells as `0`
5. **Record Coordinates**: After DFS completes, `maxRow` and `maxCol` contain the bottom-right corner
   - Add `[i, j, maxRow, maxCol]` to result list
6. **Return Result**: Convert list to 2D array and return

### DFS Function Logic
- **Base Cases**: Return if out of bounds or cell is `0` (forest/visited)
- **Track Maximum Boundaries**: 
  - If `row > maxRow`, update `maxRow = row`
  - If `col > maxCol`, update `maxCol = col`
- **Mark Visited**: Set `grid[row][col] = 0`
- **Explore Neighbors**: Recursively visit all 4 adjacent cells (up, right, down, left)

## Visual Walkthrough

Let's trace Example 1: 
```
land = [
  [1,0,0],
  [0,1,1],
  [0,1,1]
]
```

**Step 1**: Start at (0,0), find farmland (value = 1)
- Top-left: (0,0)
- Initialize: maxRow = 0, maxCol = 0
- Start DFS from (0,0)

```
Grid state:
[*,0,0]  ← Current position (0,0)
[0,1,1]
[0,1,1]
```

**DFS at (0,0)**:
- Check all 4 neighbors: all are 0 or out of bounds
- maxRow = 0, maxCol = 0 (unchanged)
- Mark (0,0) as visited (set to 0)

```
After DFS:
[0,0,0]  ← Marked as visited
[0,1,1]
[0,1,1]

Result: [[0,0,0,0]]
```

**Step 2**: Continue scanning, find farmland at (1,1)
- Top-left: (1,1)
- Initialize: maxRow = 1, maxCol = 1
- Start DFS from (1,1)

```
Grid state:
[0,0,0]
[0,*,1]  ← Current position (1,1)
[0,1,1]
```

**DFS Traversal**:
1. At (1,1): Mark as 0, explore neighbors
2. Visit (1,2): row=1, col=2 → maxCol = 2
3. Visit (2,1): row=2, col=1 → maxRow = 2
4. Visit (2,2): row=2, col=2 → maxRow = 2, maxCol = 2

```
DFS exploration order:
[0,0,0]
[0,1,2]  ← Visits (1,1) then (1,2)
[0,3,4]  ← Then (2,1) and (2,2)

After DFS:
[0,0,0]
[0,0,0]  ← All marked as visited
[0,0,0]

maxRow = 2, maxCol = 2
Result: [[0,0,0,0],[1,1,2,2]]
```

**Final Result**: `[[0,0,0,0],[1,1,2,2]]`

## Complexity Analysis

### Time Complexity
**O(m × n)** where:
- `m` is the number of rows
- `n` is the number of columns

**Reasoning:**
- We iterate through every cell in the grid: O(m × n)
- Each cell is visited at most once during DFS (marked as 0 after visiting)
- Even with nested loops and recursion, total cell visits = m × n
- DFS for all farmlands combined processes each cell exactly once

### Space Complexity
**O(m × n)** where:
- `m` is the number of rows
- `n` is the number of columns

**Reasoning:**
- **Recursion Stack**: In worst case (entire grid is one farmland in snake pattern), recursion depth is O(m × n)
- **Result Storage**: In worst case (every cell is a separate 1×1 farmland), we store m × n farmland groups, each taking O(1) space for 4 coordinates
- **In-place Modification**: We modify input grid, so no extra visited array needed

**Auxiliary Space**: O(m × n) for recursion stack in worst case

## Solution Explanation

The solution leverages the **guaranteed rectangular property** of farmlands:

### Key Components

1. **Global Variables for Tracking**:
   - `maxRow`: Tracks the maximum row index encountered during DFS
   - `maxCol`: Tracks the maximum column index encountered during DFS
   - These are reset for each new farmland group

2. **Main Algorithm Flow**:
   - **Scanning Phase**: Iterate through grid to find unvisited farmland starts
   - **Exploration Phase**: Use DFS to traverse entire farmland and track boundaries
   - **Recording Phase**: Store top-left (scan position) and bottom-right (max position)

3. **DFS Strategy**:
   - Marks cells as visited to prevent reprocessing
   - Updates maximum row/column as it explores
   - Guarantees all cells of rectangular farmland are processed

### Why This Works

Since farmlands are rectangular:
- The first cell we encounter (during left-to-right, top-to-bottom scan) is always the top-left corner
- During DFS, the maximum row and column we reach must be the bottom-right corner
- No need to track all coordinates—just the boundaries

### Optimization Notes
- In-place modification saves O(m × n) space for visited array
- Early termination in DFS when hitting boundaries or forest
- Single pass through grid with DFS ensures linear time complexity

## Full Solution

### Java Implementation
```java
class Solution {
    // Static variables to track the bottom-right corner of current farmland
    static int maxRow, maxCol;
    
    // DFS to explore farmland and find bottom-right corner
    public static void dfs(int[][] grid, int row, int col) {
        // Base case: out of bounds or not farmland (0 = forest or visited)
        if(row < 0 || col < 0 || row > grid.length - 1 || 
           col > grid[0].length - 1 || grid[row][col] == 0) {
            return;
        }
        
        // Update maximum row if current row is larger
        if(row > maxRow) maxRow = row;
        
        // Update maximum column if current column is larger
        if(col > maxCol) maxCol = col;
        
        // Mark current cell as visited (set to 0)
        grid[row][col] = 0;
        
        // Explore all 4 adjacent cells
        dfs(grid, row - 1, col);  // up
        dfs(grid, row, col + 1);  // right
        dfs(grid, row + 1, col);  // down
        dfs(grid, row, col - 1);  // left
    }
    
    public int[][] findFarmland(int[][] land) {
        List<int[]> ls = new ArrayList<>();
        
        // Scan through entire grid
        for(int i = 0; i < land.length; i++) {
            for(int j = 0; j < land[0].length; j++) {
                // Found unvisited farmland - this is top-left corner
                if(land[i][j] == 1) {
                    // Initialize max boundaries to current position
                    maxRow = i;
                    maxCol = j;
                    
                    // Explore entire farmland via DFS
                    dfs(land, i, j);
                    
                    // Record: [top-left row, top-left col, bottom-right row, bottom-right col]
                    ls.add(new int[] {i, j, maxRow, maxCol});
                }
            }
        }
        
        // Convert ArrayList to 2D array
        int[][] res = new int[ls.size()][4];
        for(int i = 0; i < ls.size(); i++) {
            for(int j = 0; j < 4; j++) {
                res[i][j] = ls.get(i)[j];
            }
        }
        
        return res;
    }
}
```

### C++ Implementation
```cpp
class Solution {
public:
    // Variables to track the bottom-right corner of current farmland
    int maxRow, maxCol;
    
    // DFS to explore farmland and find bottom-right corner
    void dfs(vector<vector<int>>& grid, int row, int col) {
        // Base case: out of bounds or not farmland (0 = forest or visited)
        if(row < 0 || col < 0 || row > grid.size() - 1 || 
           col > grid[0].size() - 1 || grid[row][col] == 0) {
            return;
        }
        
        // Update maximum row if current row is larger
        if(row > maxRow) maxRow = row;
        
        // Update maximum column if current column is larger
        if(col > maxCol) maxCol = col;
        
        // Mark current cell as visited (set to 0)
        grid[row][col] = 0;
        
        // Explore all 4 adjacent cells
        dfs(grid, row - 1, col);  // up
        dfs(grid, row, col + 1);  // right
        dfs(grid, row + 1, col);  // down
        dfs(grid, row, col - 1);  // left
    }
    
    vector<vector<int>> findFarmland(vector<vector<int>>& land) {
        vector<vector<int>> res;
        
        // Scan through entire grid
        for(int i = 0; i < land.size(); i++) {
            for(int j = 0; j < land[0].size(); j++) {
                // Found unvisited farmland - this is top-left corner
                if(land[i][j] == 1) {
                    // Initialize max boundaries to current position
                    maxRow = i;
                    maxCol = j;
                    
                    // Explore entire farmland via DFS
                    dfs(land, i, j);
                    
                    // Record: [top-left row, top-left col, bottom-right row, bottom-right col]
                    res.push_back({i, j, maxRow, maxCol});
                }
            }
        }
        
        return res;
    }
};
```

## Test Cases Analysis

| Input Grid | Farmlands | Output | Explanation |
|------------|-----------|--------|-------------|
| `[[1]]` | 1 | `[[0,0,0,0]]` | Single cell farmland |
| `[[0]]` | 0 | `[]` | No farmland |
| `[[1,1],[1,1]]` | 1 | `[[0,0,1,1]]` | One 2×2 farmland |
| `[[1,0,1],[0,0,0],[1,0,1]]` | 4 | `[[0,0,0,0],[0,2,0,2],[2,0,2,0],[2,2,2,2]]` | Four corners |
| `[[1,1,1,1]]` | 1 | `[[0,0,0,3]]` | Horizontal 1×4 farmland |
| `[[1],[1],[1],[1]]` | 1 | `[[0,0,3,0]]` | Vertical 4×1 farmland |
| `[[1,0],[1,0],[1,0]]` | 1 | `[[0,0,2,0]]` | Vertical 3×1 farmland |
| `[[1,1,0],[1,1,0],[0,0,1]]` | 2 | `[[0,0,1,1],[2,2,2,2]]` | 2×2 and 1×1 farmlands |

## Edge Cases to Consider

1. **Empty Grid**: Grid with only forests (`0`s) → return empty array
2. **Single Cell**: 1×1 grid with farmland → `[[0,0,0,0]]`
3. **Entire Grid is Farmland**: All cells are `1` → one farmland covering entire grid
4. **Horizontal Strip**: Single row farmland spanning multiple columns
5. **Vertical Strip**: Single column farmland spanning multiple rows
6. **Diagonal Cells**: Non-adjacent cells (diagonally placed) form separate farmlands
7. **Multiple Same-Size Farmlands**: Several farmlands with identical dimensions
8. **Maximum Size**: 300×300 grid to test performance
9. **Checkerboard Pattern**: Alternating `0`s and `1`s → many 1×1 farmlands
10. **Nested Rectangles**: Not possible per problem constraints (no overlapping)

## Common Test Cases

1. **Single Large Farmland**: Entire grid or most of it is one farmland
2. **Many Small Farmlands**: Grid divided into many small rectangular farmlands
3. **Sparse Farmlands**: Few scattered farmlands with lots of forest
4. **Adjacent Farmlands**: Multiple farmlands touching each other (separated by forest)
5. **Corner Farmlands**: Farmlands positioned at grid corners
6. **Border Farmlands**: Farmlands along grid edges
7. **Central Farmland**: One farmland in the middle surrounded by forest

## Common Mistakes to Avoid

1. **Forgetting to Mark Visited**: Not setting `grid[row][col] = 0` causes infinite recursion and incorrect results—each cell would be counted multiple times
2. **Not Resetting Max Variables**: Forgetting to reset `maxRow` and `maxCol` for each new farmland causes previous farmland's boundaries to leak into current calculation
3. **Assuming Non-Rectangular Shapes**: The problem guarantees rectangular farmlands; solutions handling arbitrary shapes are unnecessarily complex and may fail test cases

## Interview Relevance

1. **DFS with Boundary Tracking**: Tests ability to combine DFS traversal with state tracking (max row/col)—a common interview pattern
2. **Constraint Utilization**: Demonstrates using problem constraints (rectangular guarantee) to simplify solution
3. **Grid Problems**: Excellent practice for the ubiquitous 2D grid traversal questions in technical interviews

## What This Problem Teaches

- **Leveraging problem constraints**: The rectangular guarantee eliminates need for complex shape detection
- **Boundary tracking during DFS**: Accumulating min/max values while traversing
- **In-place modification**: Using grid itself as visited array saves space
- **2D grid traversal patterns**: Standard left-to-right, top-to-bottom scanning
- **Combining techniques**: DFS + boundary tracking + result collection
- **Global state in recursion**: Using class/global variables to track information across recursive calls
- **Early termination**: Stopping DFS at boundaries and already-visited cells

## Key Takeaways

- **Rectangular farmlands** mean we only need two corners: top-left and bottom-right
- **Top-left corner** is guaranteed to be the first cell we encounter during scan
- **Bottom-right corner** is the maximum row and column reached during DFS
- **In-place marking** (setting to 0) prevents revisiting and saves space
- **Global variables** (`maxRow`, `maxCol`) simplify tracking across recursive calls
- **Scan order matters**: Left-to-right, top-to-bottom ensures first encounter is top-left
- **DFS vs BFS**: DFS is more natural for this problem due to recursion and boundary tracking

## Problem Difficulty Analysis

**Difficulty Level**: Medium

**Skills Required**:
- Depth-First Search (DFS)
- 2D grid traversal
- Boundary tracking
- Recursion
- In-place modification
- State management across recursive calls

**Why It's Medium Difficulty**:
- Requires understanding of DFS and grid traversal
- Needs insight to track boundaries during traversal
- Must manage global state (max row/col) correctly
- Potential for bugs in boundary tracking and visited marking
- Rectangular constraint simplification is not immediately obvious

**Comparison to Related Problems**:
- Easier than "Count Sub Islands" (no grid comparison)
- Similar to "Max Area of Island" (both use DFS with tracking)
- Harder than "Number of Islands" (needs boundary coordinates, not just count)

**Related LeetCode Problems**:
- 200. Number of Islands
- 695. Max Area of Island
- 1254. Number of Closed Islands
- 1905. Count Sub Islands
- 1992. Find All Groups of Farmland (this problem)
- 463. Island Perimeter

**Time to Solve**: 
- Beginners: 40-50 minutes
- Intermediate: 20-30 minutes
- Advanced: 12-18 minutes

**Interview Tips**:
1. **Clarify the rectangular constraint** early—it's critical to the solution
2. **Explain the top-left guarantee**: First encounter during scan is always top-left
3. **Discuss boundary tracking**: How maxRow and maxCol give us bottom-right corner
4. **Walk through a small example** before coding
5. **Mention alternative approach**: Could also find top-left, then calculate bottom-right using shape
6. **Consider follow-up**: What if farmlands aren't rectangular? (More complex shape detection needed)
7. **Space optimization**: Discuss tradeoff of modifying input vs. using visited array
8. **Edge cases**: Empty grid, single cell, entire grid as farmland