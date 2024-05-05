# 206. Reverse Linked List
* **一刷:8:22(✅)**
* [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

## My Code
* 要求 **Iteratively or Recursively**, 不熟悉 Recursively

``` java
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
    public ListNode reverseList(ListNode head) {
        if(head == null) return head;
        return reverse(null, head);
    }
    private ListNode reverse(ListNode slow, ListNode fast){
        if(fast.next == null){
            fast.next = slow;
            return fast;
        }
        ListNode tmp = fast.next;
        fast.next = slow;
        return reverse(fast,tmp);
    }
}
```