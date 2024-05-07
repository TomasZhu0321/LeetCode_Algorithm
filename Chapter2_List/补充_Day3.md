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
***
# 876. Middle of the Linked List
* **一刷:6:52(✅)**
* [876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)

## My Code
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
    public ListNode middleNode(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;
        while(fast.next != null && fast.next.next != null){
            fast = fast.next.next;
            slow = slow.next;
        }
        if(fast.next != null && fast.next.next == null){
            slow = slow.next;
        }
        return slow;
    }
}
```