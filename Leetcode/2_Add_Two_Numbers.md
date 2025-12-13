# Add Two Numbers

## Platform
**LeetCode**

## Problem Link
[2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

## Problem Statement
You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

## Input Format
- `l1`: Head of the first linked list (1 ≤ number of nodes ≤ 100)
- `l2`: Head of the second linked list (1 ≤ number of nodes ≤ 100)
- Each node contains a digit (0 ≤ Node.val ≤ 9)

## Output Format
Return the head of a linked list representing the sum of the two numbers.

## Constraints
- 1 ≤ Number of nodes ≤ 100
- 0 ≤ Node.val ≤ 9
- The number represented by the linked list does not contain leading zeros (except for 0 itself)

## Example

### Example 1
**Input:** 
```
l1 = [2, 4, 3]  (represents 342)
l2 = [5, 6, 4]  (represents 465)
```
**Output:** 
```
[7, 0, 8]  (represents 807)
```
**Explanation:** 342 + 465 = 807

### Example 2
**Input:** 
```
l1 = [0]
l2 = [0]
```
**Output:** 
```
[0]
```
**Explanation:** 0 + 0 = 0

### Example 3
**Input:** 
```
l1 = [9, 9, 9, 9, 9, 9, 9]  (represents 9999999)
l2 = [9, 9, 9, 9]            (represents 9999)
```
**Output:** 
```
[8, 9, 9, 9, 0, 0, 0, 1]  (represents 10009998)
```
**Explanation:** 9999999 + 9999 = 10009998

---

## Approach: Single Pass with Carry

## Intuition
Since digits are stored in reverse order, we can simulate addition from least significant digit (head) to most significant digit (tail), just like manual addition on paper. We maintain a carry variable to handle sums ≥ 10.

## Algorithm
1. **Initialize**:
   - Create a dummy head node to simplify list construction
   - Use a pointer `temp` to build the result list
   - Initialize `carry = 0` to track carry-over from previous addition

2. **Traverse both lists simultaneously**:
   - While either list has nodes remaining:
     - Get digit from l1 (or 0 if l1 is exhausted)
     - Get digit from l2 (or 0 if l2 is exhausted)
     - Calculate sum: `carry + digit1 + digit2`
     - Extract new carry: `sum / 10`
     - Create new node with: `sum % 10`
     - Move pointers forward

3. **Handle final carry**:
   - If carry > 0 after processing all nodes, add one more node

4. **Return result**: Return `head.next` (skip dummy node)

## Complexity Analysis
- **Time Complexity**: O(max(m, n)) where m and n are the lengths of the two linked lists
  - We traverse both lists once
- **Space Complexity**: O(max(m, n)) for the result linked list
  - The result list has at most max(m, n) + 1 nodes

## Visual Example

**Input:** l1 = [2→4→3], l2 = [5→6→4]

```
Step-by-step addition:

Position 0:
  l1: 2, l2: 5, carry: 0
  sum = 0 + 2 + 5 = 7
  carry = 7 / 10 = 0
  digit = 7 % 10 = 7
  Result: [7]

Position 1:
  l1: 4, l2: 6, carry: 0
  sum = 0 + 4 + 6 = 10
  carry = 10 / 10 = 1
  digit = 10 % 10 = 0
  Result: [7→0]

Position 2:
  l1: 3, l2: 4, carry: 1
  sum = 1 + 3 + 4 = 8
  carry = 8 / 10 = 0
  digit = 8 % 10 = 8
  Result: [7→0→8]

Final: carry = 0, no additional node needed
Output: [7→0→8]
```

## Full Solution

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        // Dummy head to simplify list construction
        ListNode head = new ListNode(0);
        ListNode temp = head;  // Pointer to build the result list
        int carry = 0;         // Track carry from previous addition
        
        // Process both lists until both are exhausted
        while(l1 != null || l2 != null) {
            // Get current digits (or 0 if list is exhausted)
            int a = l1 != null ? l1.val : 0;
            int b = l2 != null ? l2.val : 0;
            
            // Calculate sum of digits plus carry
            int sum = carry + a + b;
            
            // Extract carry for next position (integer division)
            carry = sum / 10;
            
            // Create new node with the digit (remainder after removing carry)
            temp.next = new ListNode(sum % 10);
            temp = temp.next;
            
            // Move to next nodes if available
            if(l1 != null) l1 = l1.next;
            if(l2 != null) l2 = l2.next;
        }
        
        // If there's a remaining carry, add one more node
        if(carry > 0) {
            temp.next = new ListNode(carry);
        }
        
        // Return actual head (skip dummy node)
        return head.next;
    }
}
```

## Detailed Walkthrough

### Example: l1 = [9,9,9], l2 = [9,9,9,9]

```
Initial state:
- head = [0], temp = head
- carry = 0

Iteration 1:
- a = 9, b = 9, carry = 0
- sum = 0 + 9 + 9 = 18
- carry = 18 / 10 = 1
- digit = 18 % 10 = 8
- Result: [0→8]
- temp moves to node with value 8

Iteration 2:
- a = 9, b = 9, carry = 1
- sum = 1 + 9 + 9 = 19
- carry = 19 / 10 = 1
- digit = 19 % 10 = 9
- Result: [0→8→9]

Iteration 3:
- a = 9, b = 9, carry = 1
- sum = 1 + 9 + 9 = 19
- carry = 1
- digit = 9
- Result: [0→8→9→9]

Iteration 4:
- a = 0 (l1 exhausted), b = 9, carry = 1
- sum = 1 + 0 + 9 = 10
- carry = 1
- digit = 0
- Result: [0→8→9→9→0]

After loop:
- carry = 1 (still remaining)
- Add final node: [0→8→9→9→0→1]

Return head.next: [8→9→9→0→1]
This represents: 10998 (9999 + 999 = 10998) ✓
```

## Key Insights

1. **Dummy Head Pattern**: Using a dummy head simplifies edge cases and list construction
2. **Carry Handling**: Carry is naturally propagated through the loop and checked at the end
3. **Unequal Lengths**: Using ternary operator `(l1 != null ? l1.val : 0)` handles different list lengths elegantly
4. **Reverse Order Advantage**: Since digits are reversed, we process from least to most significant (natural addition order)
5. **Single Pass**: We only need one traversal through both lists

## Edge Cases Handled

1. **Different lengths**: [9,9,9] + [1] → [0,0,0,1]
2. **Final carry**: [5] + [5] → [0,1]
3. **No carry**: [2,4] + [3,5] → [5,9]
4. **All nines**: [9,9,9,9] + [9,9,9,9] → [8,9,9,9,1]
5. **Single digit**: [0] + [0] → [0]

## Common Mistakes to Avoid

1. **Forgetting final carry**: Always check `if(carry > 0)` after the loop
2. **Not handling null**: Use ternary operators or null checks
3. **Returning wrong head**: Return `head.next`, not `head` (skip dummy)
4. **Modifying input lists**: We don't modify original lists, we create new nodes
5. **Integer overflow**: Each digit is 0-9, so sum is at most 9+9+1=19 (safe)

## Alternative Approaches

### Recursive Approach (Not Recommended)
```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    return addWithCarry(l1, l2, 0);
}

private ListNode addWithCarry(ListNode l1, ListNode l2, int carry) {
    if(l1 == null && l2 == null && carry == 0) return null;
    
    int a = l1 != null ? l1.val : 0;
    int b = l2 != null ? l2.val : 0;
    int sum = a + b + carry;
    
    ListNode node = new ListNode(sum % 10);
    node.next = addWithCarry(
        l1 != null ? l1.next : null,
        l2 != null ? l2.next : null,
        sum / 10
    );
    
    return node;
}
```
**Drawback**: Uses O(max(m,n)) space on call stack

## Practice Tips

1. **Draw it out**: Visualize the addition process on paper
2. **Test edge cases**: Different lengths, carries, zeros
3. **Explain dummy head**: Interviewers love this pattern
4. **Discuss trade-offs**: Iterative vs recursive
5. **Think aloud**: Explain carry logic clearly

## Follow-Up Questions

1. **What if digits were in forward order?** → Use stack or reverse lists first
2. **Can we modify input lists?** → Usually no, but clarify constraints
3. **What about negative numbers?** → Would need sign handling logic
4. **Can we do it in-place?** → Not easily, would complicate logic significantly
5. **What if numbers are very large?** → Linked list handles arbitrary precision naturally

---

**Note**: This problem demonstrates fundamental linked list manipulation and simulates arithmetic addition. The dummy head pattern is a crucial technique that simplifies many linked list problems by eliminating special cases for the head node.