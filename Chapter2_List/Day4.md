# 24. Swap Nodes in Paris
* **一刷:40:50(❌)**
* [24. Swap Nodes in Paris](https://leetcode.com/problems/swap-nodes-in-pairs/)

## 思路
* 需要通过`虚拟头节点dummyNode` 来找到前一个的状态
* 这里最终要的就是这个`cur`,他补全了整个`swap`逻辑，并且能够自动的记录上一个状态e.g. dummy, 1, 3
![image](../Chapter2_List/img/24.JPEG)
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
    public ListNode swapPairs(ListNode head) {
        ListNode dummy = new ListNode (-1);
        dummy.next = head;
        ListNode cur = dummy;
        ListNode tmp;
        ListNode firstNode ;
        ListNode secondNode;
        while(cur.next!= null && cur.next.next != null){
            tmp = cur.next.next.next;
            firstNode = cur.next;
            secondNode = cur.next.next;
            cur.next = secondNode;
            secondNode.next = firstNode;
            firstNode.next = tmp;
            cur = firstNode;
        }
        return dummy.next;
    }
}
```
