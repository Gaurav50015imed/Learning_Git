# Add Two Numbers

## Problem Description
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

### Examples

* **Example 1:**
  * **Input:** `l1 = [2,4,3]`, `l2 = [5,6,4]`
  * **Output:** `[7,0,8]`
  * **Explanation:** 342 + 465 = 807.

* **Example 2:**
  * **Input:** `l1 = [0]`, `l2 = [0]`
  * **Output:** `[0]`

* **Example 3:**
  * **Input:** `l1 = [9,9,9,9,9,9,9]`, `l2 = [9,9,9,9]`
  * **Output:** `[8,9,9,9,0,0,0,1]`

### Constraints
* The number of nodes in each linked list is in the range `[1, 100]`.
* `0 <= Node.val <= 9`
* It is guaranteed that the list represents a number that does not have leading zeros.

---

## Solution

### Approach: Math & Linked List Traversal
Since the digits are stored in reverse order, the head of the linked list represents the least significant digit (the ones place). This naturally aligns with how addition is performed on paper, starting from the rightmost digit and carrying over to the left. 

We can traverse both linked lists simultaneously, adding the corresponding digits along with any `carry` from the previous position. A dummy node is used to simplify the creation of the resulting linked list. If one list is longer than the other, we treat the missing nodes as `0`. We continue iterating as long as there are nodes left in either list, or if there is a leftover carry.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode()
        current = dummy
        carry = 0
        
        while l1 or l2 or carry:
            val1 = l1.val if l1 else 0
            val2 = l2.val if l2 else 0
            
            total = val1 + val2 + carry
            carry = total // 10
            
            current.next = ListNode(total % 10)
            current = current.next
            
            if l1: l1 = l1.next
            if l2: l2 = l2.next
            
        return dummy.next
