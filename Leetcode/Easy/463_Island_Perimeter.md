# Island Perimeter

## 1. Platform
**LeetCode**

## 2. Problem Link
[463. Island Perimeter](https://leetcode.com/problems/island-perimeter/)

## 3. Problem Statement
You are given a 2D grid representing a map where:
- `grid[i][j] = 1` represents land
- `grid[i][j] = 0` represents water

The grid is completely surrounded by water, and there is exactly one island (i.e., one or more connected land cells). The island doesn't have "lakes", meaning the water inside isn't connected to the water around the island. One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. 

Determine the perimeter of the island.

## 4. Input Format
- A 2D integer array `grid` of size `m x n`
- Each element is either `0` (water) or `1` (land)

## 5. Output Format
- An integer representing the perimeter of the island

## 6. Constraints
- `row == grid.length`
- `col == grid[i].length`
- `1 <= row, col <= 100`
- `grid[i][j]` is `0` or `1`
- There is exactly one island in grid

## 7. Examples

### Example 1
**Input:**
```
grid = [[0,1,0,0],
        [1,1,1,0],
        [0,1,0,0],
        [1,1,0,0]]
```

**Output:** `16`

**Explanation:**
The perimeter is the 16 yellow stripes in the image below:

```
  0  1  0  0
  1  1  1  0
  0  1  0  0
  1  1  0  0
```

The island consists of connected land cells. Each edge that touches water or the boundary contributes to the perimeter.

### Example 2
**Input:**
```
grid = [[1]]
```

**Output:** `4`

**Explanation:**
A single land cell has 4 edges, all of which contribute to the perimeter.

### Example 3
**Input:**
```
grid = [[1,0]]
```

**Output:** `4`

**Explanation:**
One land cell surrounded by water has a perimeter of 4.

## 8. Approach
**Algorithm Type:** Depth-First Search (DFS) / Graph Traversal

## 9. Intuition
The key insight is that each land cell contributes to the perimeter based on how many of its sides are exposed to water or the grid boundary. For each land cell:
- If a neighbor is water or out of bounds → add 1 to perimeter
- If a neighbor is land → add 0 to perimeter

Using DFS, we traverse the island once and count all exposed edges. We mark visited cells with `-1` to avoid recounting the same cell.

## 10. Algorithm Steps

1. **Initialize** the result variable `res = 0`
2. **Iterate** through each cell in the grid
3. **Find the first land cell** (`grid[i][j] == 1`)
4. **Start DFS** from this land cell:
   - **Base Case 1:** If current position is out of bounds OR is water (`0`) → return `1` (exposed edge)
   - **Base Case 2:** If current position is already visited (`-1`) → return `0` (no contribution)
   - **Mark** current cell as visited by setting it to `-1`
   - **Recursively explore** all 4 directions (up, right, down, left)
   - **Sum** all contributions from the 4 directions
5. **Return** the total perimeter

## 11. Visual Walkthrough

Let's trace through Example 1:

```
Initial Grid:
  0  1  0  0
  1  1  1  0
  0  1  0  0
  1  1  0  0
```

**Step 1:** Find first land cell at `(0,1)`

**Step 2:** Start DFS from `(0,1)`:
- Mark `(0,1) = -1`
- Check Up `(-1,1)` → Out of bounds → +1
- Check Right `(0,2)` → Water → +1
- Check Down `(1,1)` → Land, continue DFS
- Check Left `(0,0)` → Water → +1

**Step 3:** Continue DFS traversal through all connected land cells

**Step 4:** Each boundary edge and water-adjacent edge adds 1

**Final Count:** 16 edges total

```
After DFS (all land cells marked as -1):
  0  -1  0  0
 -1  -1 -1  0
  0  -1  0  0
 -1  -1  0  0
```

## 12. Complexity Analysis

### i. Time Complexity
**O(m × n)** where m = number of rows, n = number of columns

- We iterate through the entire grid once: O(m × n)
- DFS visits each land cell exactly once: O(number of land cells)
- Overall: O(m × n)

### ii. Space Complexity
**O(m × n)** in the worst case

- **Recursive call stack:** O(m × n) in worst case when all cells are land
- **No extra space** used besides the call stack
- We modify the input grid in-place for visited marking

## 13. Solution Explanation

The solution uses a DFS approach with the following strategy:

1. **Grid Traversal:** We scan the grid to find any land cell to start DFS
2. **DFS Logic:** When we visit a land cell:
   - We mark it as visited (`-1`) to prevent revisiting
   - We explore all 4 directions
   - For each direction, if we hit water, boundary, or out-of-bounds → we count it as 1 perimeter unit
   - If we hit already visited land → we count 0 (internal edge)
3. **Perimeter Counting:** The DFS returns the sum of all exposed edges
4. **Single Island Property:** Since there's exactly one island, we only need to call DFS once

The elegance of this solution is that it combines traversal and counting in a single pass.

## 14. Full Solution

### Java Solution
```java
class Solution {
    // DFS function to calculate perimeter contribution
    public static int dfs(int[][] grid, int row, int col) {
        // Base case: out of bounds or water cell - contributes 1 to perimeter
        if(row < 0 || col < 0 || row > grid.length - 1 || col > grid[0].length - 1 || grid[row][col] == 0)   
            return 1;
        
        // Base case: already visited cell - no contribution
        if(grid[row][col] == -1) 
            return 0;
        
        // Mark current cell as visited
        grid[row][col] = -1;
        
        // Recursively explore all 4 directions and sum contributions
        return  dfs(grid, row - 1, col) +      // Up
                dfs(grid, row, col + 1) +      // Right
                dfs(grid, row + 1, col) +      // Down
                dfs(grid, row, col - 1);       // Left
    }
    
    public int islandPerimeter(int[][] grid) {
        int res = 0;
        
        // Iterate through the grid to find land cells
        for(int i = 0; i < grid.length; i++) {
            for(int j = 0; j < grid[0].length; j++) {
                if(grid[i][j] == 1) {
                    // Start DFS from the first land cell found
                    res += dfs(grid, i, j);
                }
            }
        }
        
        return res;
    }
}
```

### C++ Solution
```cpp
class Solution {
public:
    // DFS function to calculate perimeter contribution
    int dfs(vector<vector<int>>& grid, int row, int col) {
        // Base case: out of bounds or water cell - contributes 1 to perimeter
        if(row < 0 || col < 0 || row > grid.size() - 1 || col > grid[0].size() - 1 || grid[row][col] == 0)   
            return 1;
        
        // Base case: already visited cell - no contribution
        if(grid[row][col] == -1) 
            return 0;
        
        // Mark current cell as visited
        grid[row][col] = -1;
        
        // Recursively explore all 4 directions and sum contributions
        return  dfs(grid, row - 1, col) +      // Up
                dfs(grid, row, col + 1) +      // Right
                dfs(grid, row + 1, col) +      // Down
                dfs(grid, row, col - 1);       // Left
    }
    
    int islandPerimeter(vector<vector<int>>& grid) {
        int res = 0;
        
        // Iterate through the grid to find land cells
        for(int i = 0; i < grid.size(); i++) {
            for(int j = 0; j < grid[0].size(); j++) {
                if(grid[i][j] == 1) {
                    // Start DFS from the first land cell found
                    res += dfs(grid, i, j);
                }
            }
        }
        
        return res;
    }
};
```

## 15. Test Cases Analysis

| Test Case | Input Grid | Expected Output | Reasoning |
|-----------|------------|-----------------|-----------|
| Single Cell | `[[1]]` | `4` | One cell has 4 exposed edges |
| Horizontal Line | `[[1,1,1]]` | `8` | 3 cells: 2 ends contribute 3 edges each, middle contributes 2 |
| Vertical Line | `[[1],[1],[1]]` | `8` | Similar to horizontal |
| Square Island | `[[1,1],[1,1]]` | `8` | 4 cells forming square: only outer edges count |
| Complex Shape | `[[0,1,0,0],[1,1,1,0],[0,1,0,0],[1,1,0,0]]` | `16` | Multiple protruding sections |
| All Water | `[[0,0],[0,0]]` | `0` | No land cells |
| Single with Water | `[[1,0],[0,0]]` | `4` | Corner cell with 4 exposed edges |

## 16. Edge Cases to Consider

1. **Minimum Grid Size:** `1 x 1` grid with single land cell
2. **Maximum Grid Size:** `100 x 100` grid (constraint limit)
3. **Single Cell Island:** Island consisting of only one land cell
4. **Linear Island:** Island forming a straight line (horizontal or vertical)
5. **Rectangular Island:** Completely filled rectangular region
6. **L-shaped Island:** Island with concave sections
7. **Island at Corner:** Land cells positioned at grid corners
8. **Island at Edge:** Land cells along grid boundaries

## 17. Common Test Cases

1. **Standard Example:**
   ```
   [[0,1,0,0],
    [1,1,1,0],
    [0,1,0,0],
    [1,1,0,0]]
   ```
   Expected: `16`

2. **Minimal Case:**
   ```
   [[1]]
   ```
   Expected: `4`

3. **Two-Cell Island:**
   ```
   [[1,1]]
   ```
   Expected: `6`

4. **Square Island:**
   ```
   [[1,1],
    [1,1]]
   ```
   Expected: `8`

## 18. Common Mistakes to Avoid

1. **Not Marking Visited Cells:** Forgetting to mark cells as visited (`-1`) leads to infinite recursion and stack overflow. Always mark cells before recursive calls.

2. **Incorrect Boundary Conditions:** Not properly checking all boundary conditions (row < 0, col < 0, row >= grid.length, col >= grid[0].length) can cause array index out of bounds errors.

3. **Double Counting Edges:** Counting the same edge twice when traversing from different cells. The DFS approach with visited marking prevents this naturally.

## 19. Interview Relevance

1. **Fundamental Graph Problem:** Tests understanding of DFS traversal, a crucial algorithm for technical interviews at FAANG and other tech companies.

2. **Problem-Solving Pattern:** Demonstrates the "modify input to track state" pattern, which is memory-efficient and commonly used in coding interviews.

3. **Edge Case Handling:** Requires careful handling of boundary conditions, which is a key skill interviewers assess to evaluate attention to detail and defensive programming.

## 20. What This Problem Teaches

This problem reinforces several important computer science concepts:

- **Graph Traversal:** Understanding how to navigate 2D grids using DFS
- **Recursion:** Building recursive solutions with proper base cases
- **Spatial Reasoning:** Thinking about geometric properties in a grid
- **State Management:** Using in-place modification to track visited nodes
- **Boundary Conditions:** Handling edge cases and array bounds
- **Problem Decomposition:** Breaking complex problems into smaller subproblems

## 21. Key Takeaways

1. **DFS is Powerful:** DFS can efficiently solve grid-based problems with proper base cases
2. **Perimeter = Exposed Edges:** Each land cell contributes based on adjacent water/boundaries
3. **In-Place Modification:** Using `-1` to mark visited cells saves space complexity
4. **Single Pass Efficiency:** The problem can be solved in a single traversal of the grid
5. **Direction Vectors:** Exploring 4 directions (up, right, down, left) is a common pattern

## 22. Problem Difficulty Analysis

**Difficulty Level:** Easy to Medium

**Reasoning:**
- **Easy Aspects:** 
  - Clear problem statement
  - Standard DFS implementation
  - No complex data structures required
  
- **Medium Aspects:**
  - Understanding the perimeter counting logic
  - Proper handling of base cases
  - In-place modification technique

**Recommended Practice Level:** Beginners learning DFS should master this problem before moving to more complex graph traversal problems.

**Time to Solve:** 15-25 minutes for experienced programmers, 30-45 minutes for beginners.

---

*This problem is excellent preparation for interviews and builds foundational skills in graph traversal algorithms.*