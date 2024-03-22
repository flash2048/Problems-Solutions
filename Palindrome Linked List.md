# 234. Palindrome Linked List
https://leetcode.com/problems/palindrome-linked-list

Given the **head** of a singly linked list, return **true** if it is a *palindrome* or **false** otherwise.

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
    public bool IsPalindrome(ListNode head) {
        ListNode reverseList = null;
        var queueValues = new Queue<int>();
        while (head != null)
        {
            queueValues.Enqueue(head.val);
            var next = head.next;
            head.next = reverseList;
            reverseList = head;
            head = next;
        }

        while (reverseList != null)
        {
            if (reverseList.val != queueValues.Dequeue())
                return false;
            reverseList = reverseList.next;
        }

        return true;
    }
}
```