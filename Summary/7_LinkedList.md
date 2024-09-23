# 常用方法
* 添加：`list.add(x);` //末尾
* 添加中间: `list.add(index, x);` //指定index
* 添加开头: `list.addFirst(x); `//添加在开头
* 获取指定: `list.get(index);`
* 获取开头/结尾:`list.getFirst(), list.getLast()`
* 删除: `list.remove(index);`
* 删除开头/结尾:`list.removeFirst() ; list.removeLast()`
* 清空: `list.clear()`
* 反转: `Collections.reverse()` //TC: O(n); SC: O(1)

# Common Routines
## Counting the number of nodes in the linked list
## Reversing a linkedlist in-place
* Return **Prev**!
```java
public ListNode reverseList(ListNode head) {
    if (head == null) {
        return head;
    }
    ListNode prev = null;
    ListNode cur = head;
    while (cur != null) {
        ListNode tmp = cur.next;
        cur.next = prev;
        prev = cur;
        cur = tmp;
    }
    return prev;
}
```
## Finding the middle node of the linked list using two pointer(fast/slow)
* **The termination of the while loop** is (fast!=null && fast.next!=null) ==> This can ensure if there are two middle nodes, we can return the second one

```java
    public ListNode middleNode(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        return slow;
    }
```
## Merge two linked lists together
* prev 来确保 list的顺序
```java
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode dummy = new ListNode (-1, null);
        ListNode prev = dummy;
        while (list1 != null && list2 != null) {
            if (list1.val < list2.val) {
                prev.next = list1;
                list1 = list1.next;
            } else {
                prev.next = list2;
                list2 = list2.next;
            }
            prev = prev.next;
        }
        prev.next = list1 == null ? list2 : list1;
        return dummy.next;
    }
```

# Corner Case
* Empty Linked list
* Single Node 
* Two Nodes
* Linked List has **cycles**

# Techniques
## Dummy Nodes
## Two Pointers
### Getting the Kth from last node
* Have two pointers, where one is k nodes ahead of the other. When the node ahead reaches the end, the other node is k nodes behind
### Detecting cycles
* Have two pointers, where one pointer increments twice as much as the other, if the two pointers meet, means that there is a cycle
### Getting the middle node
* Have two pointers, where one pointer increments twice as much as the other. When the faster node reaches the end of the list, the slower node will be at the middle
## Elegant modification operations
### Truncate a list 
* Set the next pointer to null at the last element
