# Maximum Number of Fish in a Grid

## Platform

**LeetCode**

## Problem Link

[https://leetcode.com/problems/maximum-number-of-fish-in-a-grid/](https://leetcode.com/problems/maximum-number-of-fish-in-a-grid/)

## Problem Statement

You are given a 2D grid where each cell contains a non-negative integer representing the number of fish in that cell. A value of `0` represents water with no fish.

You can start fishing from any cell that contains fish. From that cell, you may move **up, down, left, or right** to adjacent cells, as long as those cells also contain fish.

The objective is to determine the **maximum total number of fish** you can collect by fishing in a single connected region.

---

## Input Format

* A 2D integer matrix `grid` of size `m × n`.

---

## Output Format

* Return a single integer representing the maximum fish that can be collected.

---

## Constraints

* 1 ≤ m, n ≤ 10
* 0 ≤ grid[i][j] ≤ 100

---

## Examples

### Example 1

**Input**

```
1 2 0
3 4 5
0 6 0
```

**Output**

```
21
```

**Explanation**
All non-zero cells are connected, so the total fish collected is:
`1 + 2 + 3 + 4 + 5 + 6 = 21`

---

### Example 2

**Input**

```
0 0 0
0 7 0
0 0 0
```

**Output**

```
7
```

---

## Approach (Algorithm Type)

**Depth-First Search on Grid (Connected Component Sum)**

---

## Intuition

Each group of connected non-zero cells forms an independent fishing region. The problem reduces to computing the sum of values in each connected component and returning the maximum sum among them.

---

## Algorithm Description

The grid is scanned cell by cell. When a cell with fish is found, a DFS traversal is initiated to collect all connected fish in that region. Each visited cell is marked as `0` to avoid revisiting. The total fish collected from that traversal is compared against the current maximum.

---

## Visual Walkthrough

For the grid:

```
1 2 0
3 4 5
0 6 0
```

* Start DFS at cell `(0,0)`
* Traverse all adjacent non-zero cells
* Accumulate fish count during traversal
* Mark visited cells as `0`

Final accumulated sum = 21

---

## Complexity Analysis

### Time Complexity

* **O(m × n)** since each cell is visited at most once.

### Space Complexity

* **O(m × n)** in the worst case due to recursion stack during DFS.

---

## Solution Explanation

The solution relies on DFS to explore each connected fishing region. By marking cells as visited directly in the grid, extra memory for a visited array is avoided. The DFS returns the total fish count for a region, making it easy to track the maximum.

---

## Full Solution (with Commented Code)

### Java Implementation

```java
class Solution {
    // DFS to collect fish from a connected region
    public static int dfs(int[][] grid, int row, int col) {
        // Boundary check and water check
        if (row < 0 || col < 0 || row > grid.length - 1 || col > grid[0].length - 1 || grid[row][col] == 0)
            return 0;

        // Collect fish from current cell
        int t = grid[row][col];
        
        // Mark cell as visited
        grid[row][col] = 0;

        // Explore all four directions
        return t + dfs(grid, row - 1, col)
                 + dfs(grid, row, col + 1)
                 + dfs(grid, row + 1, col)
                 + dfs(grid, row, col - 1);
    }

    public int findMaxFish(int[][] grid) {
        int maxFish = 0;

        // Traverse the grid
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                // Start DFS when fish is found
                if (grid[i][j] > 0) {
                    maxFish = Math.max(maxFish, dfs(grid, i, j));
                }
            }
        }
        return maxFish;
    }
}
```

### C++ Implementation

```cpp
class Solution {
public:
    // DFS to collect fish from a connected region
    int dfs(vector<vector<int>>& grid, int row, int col) {
        // Boundary check and water check
        if (row < 0 || col < 0 || row > grid.size() - 1 || col > grid[0].size() - 1 || grid[row][col] == 0)
            return 0;

        // Collect fish from current cell
        int t = grid[row][col];
        
        // Mark cell as visited
        grid[row][col] = 0;

        // Explore all four directions
        return t + dfs(grid, row - 1, col)
                 + dfs(grid, row, col + 1)
                 + dfs(grid, row + 1, col)
                 + dfs(grid, row, col - 1);
    }

    int findMaxFish(vector<vector<int>>& grid) {
        int maxFish = 0;

        // Traverse the grid
        for (int i = 0; i < grid.size(); i++) {
            for (int j = 0; j < grid[0].size(); j++) {
                // Start DFS when fish is found
                if (grid[i][j] > 0) {
                    maxFish = max(maxFish, dfs(grid, i, j));
                }
            }
        }
        return maxFish;
    }
};
```

---

## Test Cases Analysis

| Grid Description | Expected Output | Reason             |
| ---------------- | --------------- | ------------------ |
| All zeros        | 0               | No fish present    |
| Single non-zero  | Cell value      | One region         |
| Multiple regions | Maximum sum     | Choose best region |

---

## Edge Cases to Consider

* Grid with no fish
* Grid with only one fishing cell
* All cells connected
* Maximum grid size

---

## Common Mistakes to Avoid

* Forgetting to mark visited cells
* Revisiting the same region multiple times
* Incorrect boundary checks

---

## Interview Relevance

* Strong example of DFS on grids
* Demonstrates connected component analysis
* Highlights in-place modification techniques

---

## What This Problem Teaches

* DFS-based aggregation problems
* Grid traversal fundamentals
* Efficient use of recursion

---

## Key Takeaways

* Each fishing region is independent
* DFS naturally computes connected sums
* In-place marking simplifies logic

---

## Problem Difficulty Analysis

**Difficulty Level:** Medium

The challenge lies in correctly traversing connected regions and managing state efficiently.
