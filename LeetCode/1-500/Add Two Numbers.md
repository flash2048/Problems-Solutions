# 2. Add Two Numbers
https://leetcode.com/problems/add-two-numbers

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg)

```
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```

**Example 2:**

```
Input: l1 = [0], l2 = [0]
Output: [0]
```

**Example 3:**

```
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```

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
    public ListNode AddTwoNumbers(ListNode l1, ListNode l2) {
        var result = new ListNode();

        var l1Next = l1;
        var l2Next = l2;
        var remainder = 0;
        var resultNext = result;

        while (l1Next != null || l2Next != null)
        {
            var sum = (l1Next?.val ?? 0) + (l2Next?.val ?? 0) + remainder;
            l1Next = l1Next?.next;
            l2Next = l2Next?.next;

            resultNext.val = sum % 10;
            remainder = sum / 10;

            if (l1Next != null || l2Next != null)
                resultNext.next = new ListNode();
            else
            {
                if (remainder > 0)
                    resultNext.next = new ListNode(remainder);
            }
            resultNext = resultNext.next;
        }

        return result;
    }
}
```