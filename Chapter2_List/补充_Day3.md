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
***
# 160. Intersection of Two Linked Lists
* **一刷:28:22(❌)**
* [160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)

## 错误反思
* 两个ListNode即使null，也可以是相等的，所以不用害怕null. 如果两个点都在null上，`直接返回本身(null)`就可以了！
* 错误反思：
  * 将问题复杂化了，判断条件不用将`indexA.next != null || indexB.next != null)`领出来, 这样反而是错误的
```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode indexA = headA;
        ListNode indexB = headB;
        while (indexA!=indexB) {
            if (indexA == null) {
                indexA = headB;
            } else {
                indexA = indexA.next;
            }
            if (indexB == null) {
                indexB = headA;
            } else {
                indexB = indexB.next;
            }
        }
        return indexA;
    }
}
```

***
# 141. Linked List Cycle (Linked List Cycle II)
* **一刷:8:22(✅)**
* [141. Linked List Cycle (Linked List Cycle II)](https://leetcode.com/problems/linked-list-cycle/)

## 技巧
* 指针类移动list的题
  * 不要害怕将 指针移到null的时候，作为条件
  * 越前的在判断语句中应放在越前 e.g. `if(point != null && point.next != null)`
## My Code
```java 
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head == null || head.next == null) return false;
        ListNode slow = head;
        ListNode fast = head.next;
        while(fast!= null && fast.next != null){
            if(fast == slow) return true;
            fast = fast.next.next;
            slow = slow.next;
        }
        return false;
    }
}
```
***
# 92. Reverse Linked List II
* **一刷:38:22(✅)**
* [92. Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii/)

## My Code
```java
class Solution {
    public ListNode reverseBetween(ListNode head, int left, int right) {
        if (head.next == null || left == right)
            return head;

        ListNode dummy = head;
        ListNode first = head;
        ListNode last = head;
        int position = 1;
        while (position + 1 < left) {
            first = first.next;
            last = last.next;
            position++;
        }
        while (position < right) {
            last = last.next;
            position++;
        }
        ListNode end = last.next;
        last.next = null;
        ListNode reList;
        if (left == 1) {
            reList = first;
            reList = reverse(reList);
            first.next = end;
            return reList;
        } else {
            reList = first.next;
            ListNode res = reverse(reList);
            first.next = res;
            reList.next = end;
        }
        return dummy;
    }

    private ListNode reverse(ListNode head) {
        if (head == null)
            return null;
        ListNode slow = null;
        ListNode fast = head;
        while (fast.next != null) {
            ListNode tmp = fast.next;
            fast.next = slow;
            slow = fast;
            fast = tmp;
        }
        fast.next = slow;
        return fast;
    }
}
```
