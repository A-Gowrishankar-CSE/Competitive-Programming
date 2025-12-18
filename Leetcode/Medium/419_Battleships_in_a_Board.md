# Battleships in a Board

## Platform

**LeetCode**

## Problem Link

[https://leetcode.com/problems/battleships-in-a-board/](https://leetcode.com/problems/battleships-in-a-board/)

## Problem Statement

You are given a 2D board representing a battlefield. Each cell contains either:

* `'X'` representing part of a battleship, or
* `'.'` representing empty water.

Battleships are placed on the board according to the following rules:

* Each battleship occupies consecutive cells either **horizontally** or **vertically**.
* Battleships are separated by at least one cell of water in all directions.

The task is to count the number of battleships on the board.

---

## Input Format

* A 2D character matrix `board` of size `m × n`.

---

## Output Format

* Return a single integer representing the total number of battleships.

---

## Constraints

* 1 ≤ m, n ≤ 200
* `board[i][j]` is either `'X'` or `'.'`
* Battleships do not touch each other

---

## Examples

### Example 1

**Input**

```
X..X
...X
...X
```

**Output**

```
2
```

**Explanation**

* One battleship is placed horizontally at the top row.
* One battleship is placed vertically in the last column.

---

### Example 2

**Input**

```
.
```

**Output**

```
0
```

---

## Approach (Algorithm Type)

**Depth-First Search (DFS) with In-place Marking**

---

## Intuition

Each battleship forms a connected component of `'X'` cells extending only to the right or downward. Once a battleship is discovered, all its connected parts can be marked as visited to prevent double counting.

---

## Algorithm Description

The board is traversed cell by cell. When an unvisited `'X'` is encountered, it represents the start of a new battleship. A DFS is launched to mark all contiguous `'X'` cells belonging to that battleship. The count is incremented once per DFS invocation.

---

## Visual Walkthrough

For the board:

```
X..X
...X
...X
```

* Start at `(0,0)` → DFS marks the horizontal battleship
* Move to `(0,3)` → DFS marks the vertical battleship

Final count = 2

---

## Complexity Analysis

### Time Complexity

* **O(m × n)** where `m` is the number of rows and `n` is the number of columns.
* Each cell is visited at most once.

### Space Complexity

* **O(m × n)** in the worst case due to recursion stack in DFS.
* No extra data structures are used beyond recursion.

---

## Solution Explanation

The solution modifies the board directly by replacing visited `'X'` cells with `'.'`. This ensures that each battleship is counted exactly once. DFS only explores rightward and downward directions, which is sufficient due to the problem constraints.

---

## Full Solution (with Commented Code)

### Java Implementation

```java
class Solution {
    // Depth First Search to mark the entire battleship as visited
    public static void dfs(char[][] board, int row, int col) {
        // Boundary check and water check
        if (row > board.length - 1 || col > board[0].length - 1 || board[row][col] == '.')
            return;

        // Mark current cell as visited
        board[row][col] = '.';

        // Explore downward and rightward cells
        dfs(board, row + 1, col);
        dfs(board, row, col + 1);
    }

    public int countBattleships(char[][] board) {
        int count = 0;

        // Traverse the entire board
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                // Found the start of a battleship
                if (board[i][j] == 'X') {
                    dfs(board, i, j);
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
    // Depth First Search to mark the entire battleship as visited
    void dfs(vector<vector<char>>& board, int row, int col) {
        // Boundary check and water check
        if (row > board.size() - 1 || col > board[0].size() - 1 || board[row][col] == '.')
            return;

        // Mark current cell as visited
        board[row][col] = '.';

        // Explore downward and rightward cells
        dfs(board, row + 1, col);
        dfs(board, row, col + 1);
    }

    int countBattleships(vector<vector<char>>& board) {
        int count = 0;

        // Traverse the entire board
        for (int i = 0; i < board.size(); i++) {
            for (int j = 0; j < board[0].size(); j++) {
                // Found the start of a battleship
                if (board[i][j] == 'X') {
                    dfs(board, i, j);
                    count++;
                }
            }
        }
        return count;
    }
};
```

---

## Test Cases Analysis

| Board Configuration | Expected Output | Reason                     |
| ------------------- | --------------- | -------------------------- |
| All water           | 0               | No battleships             |
| Single `X`          | 1               | One-cell battleship        |
| Horizontal ship     | 1               | Single connected component |
| Multiple ships      | Correct count   | DFS prevents double count  |

---

## Edge Cases to Consider

* Empty board
* Board with only water cells
* Board with maximum dimensions
* Single row or single column board

---

## Common Mistakes to Avoid

* Counting connected `'X'` cells multiple times
* Forgetting to mark visited cells
* Exploring unnecessary directions

---

## Interview Relevance

* Demonstrates DFS traversal on grids
* Tests understanding of connected components
* Evaluates in-place modification techniques

---

## What This Problem Teaches

* Grid traversal using DFS
* Efficient counting of connected components
* Leveraging problem constraints to simplify logic

---

## Key Takeaways

* Each battleship is a distinct connected component
* In-place marking avoids extra memory usage
* DFS is a natural fit for grid-based problems

---

## Problem Difficulty Analysis

**Difficulty Level:** Medium

While the logic is straightforward, careful handling of traversal and constraints is required to avoid overcounting.
