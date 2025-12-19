# Solution

## Platform

LeetCode

## Problem Link

[https://leetcode.com/problems/clone-graph/](https://leetcode.com/problems/clone-graph/)

## Problem Statement

You are given a reference to a node in a connected undirected graph.
Each node contains a value and a list of its neighbors.

Your task is to create a **deep copy** of the graph and return the reference to the cloned node.

A deep copy means:

* Every node in the new graph is a **newly created object**
* No node in the cloned graph references an original node

## Input Format

* A reference to a `Node` representing a graph
* Each node contains:

  * `val` → integer value
  * `neighbors` → list of adjacent nodes

## Output Format

* A reference to the cloned graph’s starting node

## Constraints

* The graph is connected
* The graph may contain cycles
* Node values are unique
* The number of nodes is finite

## Examples

### Example 1

Input (conceptual graph):

```
1 -- 2
|    |
4 -- 3
```

Explanation
Each node is connected bidirectionally.
The cloned graph must reproduce the same structure using **new node objects**.

Output
A new graph with identical connections and values, but no shared references with the original.

### Example 2

Input

```
Empty graph (null)
```

Output

```
null
```

## Approach

Depth-First Search (DFS) with hashing (visited map).

## Intuition

Graphs may contain **cycles**, so a naive recursive clone would result in infinite recursion.

To prevent this:

* Maintain a map from **original node → cloned node**
* If a node has already been cloned, reuse it instead of creating a new one

This guarantees:

* Each node is cloned exactly once
* Cycles are handled safely

## Algorithm Steps

* If the input node is `null`, return `null`
* Create a clone of the current node
* Store the mapping between original and cloned nodes
* Traverse each neighbor:

  * If already cloned, attach the existing clone
  * Otherwise, recursively clone the neighbor
* Return the cloned node

## Visual Walkthrough

Original graph:

```
1 ---- 2
|      |
4 ---- 3
```

### Step 1: Start at Node 1

* Clone node `1`
* Store mapping:

  ```
  1 → 1'
  ```

### Step 2: Visit Neighbor Node 2

* Clone node `2`
* Store mapping:

  ```
  2 → 2'
  ```
* Attach `2'` to `1'`

### Step 3: Visit Node 3

* Clone node `3`
* Store mapping:

  ```
  3 → 3'
  ```

### Step 4: Encounter Node 1 Again (Cycle)

* Node `1` already exists in map
* Reuse `1'` instead of cloning again

### Final Result

```
1' ---- 2'
 |       |
4' ---- 3'
```

No cloned node references any original node.

## Complexity Analysis

### Time Complexity

O(V + E)
Each vertex and edge is visited once.

### Space Complexity

O(V)
Used for the recursion stack and the hash map storing cloned nodes.

## Solution Explanation

The solution performs a DFS traversal of the graph.
A hash map tracks which nodes have already been cloned, ensuring:

* No duplicate clones
* Safe handling of cycles

Whenever a node is revisited, the previously created clone is reused.

## Full Solution

### Java Implementation (Heavily Commented)

```java
class Solution {

    // Map to store the mapping from original nodes to their cloned counterparts
    static Map<Node, Node> map = new HashMap<>();

    public Node cloneGraph(Node node) {

        // Base case:
        // If the input node is null, there is nothing to clone
        if (node == null) return null;

        // Create a new node with the same value as the original
        Node nn = new Node(node.val);

        // Store the mapping from original node to cloned node
        // This prevents re-cloning the same node and handles cycles
        map.put(node, nn);

        // Iterate over all neighbors of the original node
        for (int i = 0; i < node.neighbors.size(); i++) {

            // If the neighbor is already cloned,
            // directly add the cloned neighbor to the current node's neighbors
            if (map.containsKey(node.neighbors.get(i))) {
                nn.neighbors.add(map.get(node.neighbors.get(i)));
            }
            // Otherwise, recursively clone the neighbor
            else {
                nn.neighbors.add(cloneGraph(node.neighbors.get(i)));
            }
        }

        // Return the cloned node
        return nn;
    }
}
```

### C++ Implementation (Heavily Commented)

```cpp
class Solution {
public:

    // Map to keep track of original nodes and their clones
    map<Node*, Node*> map;

    Node* cloneGraph(Node* node) {

        // Base case:
        // If the input node is null, return null
        if (node == NULL) return NULL;

        // Create a new node with the same value
        Node* nn = new Node(node->val);

        // Store mapping from original node to cloned node
        // This helps in handling cycles and avoiding duplicate cloning
        map[node] = nn;

        // Traverse all neighbors of the current node
        for (int i = 0; i < node->neighbors.size(); i++) {

            // If the neighbor has already been cloned,
            // reuse the cloned version
            if (map.contains(node->neighbors[i])) {
                nn->neighbors.push_back(map[node->neighbors[i]]);
            }
            // Otherwise, recursively clone the neighbor
            else {
                nn->neighbors.push_back(cloneGraph(node->neighbors[i]));
            }
        }

        // Return the cloned node
        return nn;
    }
};
```

## Test Cases Analysis

| Graph Type   | Description     | Expected Outcome   |
| ------------ | --------------- | ------------------ |
| Single node  | No neighbors    | Single cloned node |
| Cycle graph  | Node revisited  | No infinite loop   |
| Linear graph | Chain structure | Exact deep copy    |
| Null input   | Empty graph     | Null output        |

## Edge Cases to Consider

* Graph with a single node and no neighbors
* Graph containing cycles
* Null input graph

## Common Test Cases

* Fully connected graph
* Sparse graph
* Graph with self-loops

## Common Mistakes to Avoid

* Not tracking visited nodes
* Creating duplicate clones
* Forgetting to handle cycles

## Interview Relevance

* Very common graph problem
* Tests understanding of DFS and hashing
* Evaluates deep copy concepts

## What This Problem Teaches

* How to clone cyclic data structures
* Safe recursion using memoization
* Graph traversal fundamentals

## Key Takeaways

* Always track visited nodes in graph cloning
* Hash maps are essential for cycle handling
* DFS naturally fits graph duplication problems

## Problem Difficulty Analysis

This is a **Medium-level** problem.
The logic is straightforward, but correctness depends on handling cycles and node reuse carefully.