# 143. Reorder List
* **一刷:25:22(✅)**
* [143. Reorder List](https://leetcode.com/problems/reorder-list/)

## My Code
* 注意：需要在最后将ListNode 指向null
``` java
class Solution {
    public void reorderList(ListNode head) {
        Deque<ListNode> dq = new LinkedList<>();
        ListNode move = head;
        // put list into dq
        while (move != null) {
            dq.add(move);
            move = move.next;
        }
        // construct a new resList
        ListNode res = head;
        while (!dq.isEmpty()) {
            ListNode front = dq.poll();
            res.next = front;
            res = res.next;
            if (dq.isEmpty()) {
                break;
            } else {
                ListNode end = dq.pollLast();
                res.next = end;
                res = res.next;
            }
        }
        res.next = null;
        return;
    }
}
```