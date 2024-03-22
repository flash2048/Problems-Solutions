# 206. Reverse Linked List
https://leetcode.com/problems/reverse-linked-list/

Given the `head` of a singly linked list, reverse the list, and return the reversed list.

```csharp
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int val=0, ListNode next=null) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */
public class Solution {
    public ListNode ReverseList(ListNode head) {
        ListNode result = null;
        while (head != null)
        {
            var next = head.next;
            head.next = result;
            result = head;
            head = next;
        }
        return result;
    }
}
```