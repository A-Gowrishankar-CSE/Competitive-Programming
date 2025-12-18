# Surrounded Regions

## Platform

LeetCode

## Problem Link

[130. Surrounded Regions](https://leetcode.com/problems/surrounded-regions/)

## Problem Statement

You are given an `m × n` board containing characters `'X'` and `'O'`.
Your task is to capture all regions of `'O'` that are **completely surrounded** by `'X'`.

A region is considered surrounded if it is **not connected to any boundary `'O'`**.
All such surrounded `'O'` cells must be flipped to `'X'`.
Cells that are connected directly or indirectly to a boundary `'O'` must remain unchanged.

The board must be modified **in place**.

## Input Format

A two-dimensional character matrix `board` of size `m × n`, where each cell contains either `'X'` or `'O'`.

## Output Format

The same board, modified in place such that all surrounded regions are captured.

## Constraints

* `1 ≤ m, n ≤ 200`
* `board[i][j] ∈ {'X', 'O'}`
* The solution must not use extra memory proportional to the board size

## Examples

### Example 1

Input

```
X X X X
X O O X
X X O X
X O X X
```

Explanation

* The `'O'` cells in the middle are fully surrounded by `'X'`.
* The `'O'` at the boundary (row 3, column 0) is connected to the border and cannot be captured.

Output

```
X X X X
X X X X
X X X X
X O X X
```

### Example 2

Input

```
O O
O O
```

Explanation
All `'O'` cells touch the boundary directly or indirectly, so no cell is flipped.

Output

```
O O
O O
```

## Approach

Depth-First Search (DFS) with boundary traversal and temporary marking.

## Intuition

Instead of trying to detect surrounded regions directly, the problem becomes simpler if we reverse the logic:

* Any `'O'` connected to the boundary **cannot** be captured.
* Therefore, first identify and protect all `'O'` cells reachable from the boundary.
* After protecting these cells, any remaining `'O'` must be fully surrounded and can be safely flipped.

A temporary marker is used to distinguish protected cells from capturable ones.

## Algorithm Steps

* Store the board dimensions.
* Traverse the first and last rows and perform DFS for every `'O'`.
* Traverse the first and last columns and perform DFS for every `'O'`.
* During DFS, temporarily mark safe `'O'` cells as `'T'`.
* Traverse the entire board:

  * Convert remaining `'O'` cells to `'X'`.
  * Convert `'T'` cells back to `'O'`.

## Visual Walkthrough

Consider the following board:

```
X  X  X  X
X  O  O  X
X  X  O  X
X  O  X  X
```

### Step 1: Identify Boundary Cells

Boundary cells are those located on:

* The first row
* The last row
* The first column
* The last column

Boundary `'O'` cells **cannot be captured** because they are not fully surrounded.

In this board, the boundary `'O'` is:

```
(3, 0)
```

Visual marking of boundary `'O'`:

```
X  X  X  X
X  O  O  X
X  X  O  X
O  X  X  X
```

### Step 2: DFS from Boundary `'O'`

Start DFS from every boundary `'O'` and mark all connected `'O'` cells as **temporarily safe (`'T'`)**.

After DFS marking:

```
X  X  X  X
X  O  O  X
X  X  O  X
T  X  X  X
```

Only the boundary-connected region is marked as safe.

### Step 3: Identify Capturable Regions

Now observe the board:

* Any `'O'` **not marked as `'T'`** is fully surrounded.
* These cells must be captured.

Surrounded `'O'` cells:

```
(1,1), (1,2), (2,2)
```

### Step 4: Final Transformation

Perform a full board scan:

* Convert remaining `'O'` → `'X'`
* Convert `'T'` → `'O'`

Final board:

```
X  X  X  X
X  X  X  X
X  X  X  X
O  X  X  X
```

### Key Visual Insight

```
Boundary-connected O  →  Safe (never flipped)
Inner O only          →  Captured (flipped to X)
```

### Why This Works

* Surrounded regions **cannot reach the boundary**.
* DFS ensures all reachable safe cells are protected first.
* The final sweep cleanly separates safe and unsafe regions.

## Complexity Analysis

### Time Complexity

O(m × n)
Each cell is visited at most once during DFS and once during the final traversal.

### Space Complexity

O(m × n) in the worst case due to recursive DFS call stack.

## Solution Explanation

The implementation uses DFS to mark all boundary-connected `'O'` cells as safe using a temporary marker `'T'`.
After marking, the board is scanned to flip all unsafe `'O'` cells to `'X'` and restore safe cells back to `'O'`.
This ensures correctness while maintaining in-place modification.

## Full Solution

### Java Implementation (Heavily Commented)

```java
class Solution {

    // Number of rows in the board
    static int m;

    // Number of columns in the board
    static int n;

    // Depth-First Search used to mark boundary-connected 'O' cells
    public static void dfs(char[][] board, int row, int col) {

        // Base case:
        // Stop recursion if the cell is out of bounds,
        // or if the cell is already 'X' (blocked),
        // or if the cell is already marked as temporary 'T'
        if (row < 0 || col < 0 || row >= m || col >= n ||
            board[row][col] == 'X' || board[row][col] == 'T') {
            return;
        }

        // Mark the current cell as temporarily safe
        // 'T' indicates this 'O' is connected to the boundary
        board[row][col] = 'T';

        // Explore the neighboring cells in all four directions
        dfs(board, row - 1, col); // up
        dfs(board, row, col + 1); // right
        dfs(board, row + 1, col); // down
        dfs(board, row, col - 1); // left
    }

    // Main method to solve the problem
    public void solve(char[][] board) {

        // Store board dimensions
        m = board.length;
        n = board[0].length;

        // Traverse the first and last rows
        // Any 'O' here cannot be captured
        for (int col = 0; col < n; col++) {
            if (board[0][col] == 'O') {
                dfs(board, 0, col);
            }
            if (board[m - 1][col] == 'O') {
                dfs(board, m - 1, col);
            }
        }

        // Traverse the first and last columns
        // Any 'O' here cannot be captured
        for (int row = 0; row < m; row++) {
            if (board[row][0] == 'O') {
                dfs(board, row, 0);
            }
            if (board[row][n - 1] == 'O') {
                dfs(board, row, n - 1);
            }
        }

        // Final pass over the board
        // - Convert remaining 'O' to 'X' (captured)
        // - Restore 'T' back to 'O' (safe)
        for (int row = 0; row < m; row++) {
            for (int col = 0; col < n; col++) {
                if (board[row][col] == 'O') {
                    board[row][col] = 'X';
                } else if (board[row][col] == 'T') {
                    board[row][col] = 'O';
                }
            }
        }
    }
}
```

### C++ Implementation (Heavily Commented)

```cpp
class Solution {
public:
    int m; // number of rows
    int n; // number of columns

    // DFS to mark boundary-connected 'O' cells
    void dfs(vector<vector<char>>& board, int row, int col) {

        // Stop if out of bounds or cell is not eligible
        if (row < 0 || col < 0 || row >= m || col >= n ||
            board[row][col] == 'X' || board[row][col] == 'T') {
            return;
        }

        // Mark cell as temporarily safe
        board[row][col] = 'T';

        // Visit neighboring cells
        dfs(board, row - 1, col); // up
        dfs(board, row, col + 1); // right
        dfs(board, row + 1, col); // down
        dfs(board, row, col - 1); // left
    }

    void solve(vector<vector<char>>& board) {

        // Store dimensions
        m = board.size();
        n = board[0].size();

        // First and last rows
        for (int col = 0; col < n; col++) {
            if (board[0][col] == 'O') dfs(board, 0, col);
            if (board[m - 1][col] == 'O') dfs(board, m - 1, col);
        }

        // First and last columns
        for (int row = 0; row < m; row++) {
            if (board[row][0] == 'O') dfs(board, row, 0);
            if (board[row][n - 1] == 'O') dfs(board, row, n - 1);
        }

        // Final conversion pass
        for (int row = 0; row < m; row++) {
            for (int col = 0; col < n; col++) {
                if (board[row][col] == 'O') {
                    board[row][col] = 'X';
                } else if (board[row][col] == 'T') {
                    board[row][col] = 'O';
                }
            }
        }
    }
};
```

## Test Cases Analysis

| Scenario          | Input Pattern          | Expected Result |
| ----------------- | ---------------------- | --------------- |
| All X             | No O present           | Board unchanged |
| All O             | All boundary-connected | Board unchanged |
| Inner region      | O fully enclosed       | Converted to X  |
| Single row/column | Boundary only          | No conversion   |

## Edge Cases to Consider

* Board with one row or one column
* Board filled entirely with `'X'`
* Board filled entirely with `'O'`

## Common Test Cases

* Mixed grids with isolated inner regions
* Large grids with multiple enclosed areas

## Common Mistakes to Avoid

* Flipping boundary-connected `'O'` cells
* Forgetting to restore temporary markers
* Missing boundary traversal

## Interview Relevance

* Common DFS/BFS grid traversal problem
* Tests in-place modification techniques
* Frequently asked in coding interviews

## What This Problem Teaches

* How reversing the problem perspective simplifies logic
* Efficient use of DFS in 2D grids
* Safe in-place transformations

## Key Takeaways

* Always protect boundary-connected components first
* Temporary marking avoids extra memory usage
* DFS is ideal for connected-region problems

## Problem Difficulty Analysis

This is a **Medium-level** problem.
The algorithm is conceptually simple, but correctness depends on careful boundary handling and traversal order.