# 203. Remove Linked List Elements
* **一刷:5:50(✅)**
* [203. Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements/description/)

## My Code
* 注意：我`赋值 node是能够对结果产生影响的. ListNod cur = head`
  
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
    public ListNode removeElements(ListNode head, int val) {
        ListNode res = new ListNode(-1, head);
        ListNode pre = res;
        ListNode cur = head;
        while(cur!= null){
            if(cur.val == val){
                pre.next = cur.next;
            }
            else{
                pre = cur;
            }
            cur = cur.next;
        }
        return res.next;
    }
}
```

## 707. Design Linked List
* **一刷:125:50(❌)**
* [707. Design Linked List](https://leetcode.com/problems/design-linked-list/description/)

## 错误点
### 1. 需要通过内置一个size来判断index的范围
### 2. addAtIndex 的index是可以在size的！（相当于添加在末尾）
### 3. `cur.next = xxx` 一定要放在最后!!!!! (不然就是先赋值了)

```java
class ListNode {
    int val;
    ListNode prev;
    ListNode next;
    ListNode (){}
    ListNode (int val){this.val = val;}
    ListNode (int val, ListNode prev, ListNode next){
        this.val = val;
        this.prev = prev;
        this.next = next;
    }
}
class MyLinkedList {
    ListNode dummy;
    int size;
    public MyLinkedList() {
        dummy = new ListNode (-1,null,null);
        dummy.prev = dummy;
        dummy.next = dummy;
        size = 0;
    }
    
    public int get(int index) {
        if(index < 0 || index >= size){return -1;}
        ListNode cur = dummy;
        for(int i=0; i<= index; i++){
            cur = cur.next; 
        }
        return cur.val;
    }
    
    public void addAtHead(int val) {
        ListNode tmp = new ListNode (val, dummy, dummy.next);
        dummy.next.prev = tmp;
        dummy.next = tmp;
        size ++;
    }
    
    public void addAtTail(int val) {
        ListNode tmp = new ListNode (val, dummy.prev, dummy);
        dummy.prev.next = tmp;
        dummy.prev = tmp;
        size ++;
    }
    
    public void addAtIndex(int index, int val) {
        if(index < 0){
            index = 0;
        }
        if(index > size){return ;}
        ListNode cur = dummy;
        while(index > 0){
            index --;
            cur = cur.next;
        }
        ListNode tmp = new ListNode (val, cur, cur.next);
        cur.next.prev = tmp;
        cur.next = tmp;
        size ++;
    }
    
    public void deleteAtIndex(int index) {
        if(index < 0 || index >= size){return ;}
        ListNode cur = dummy;
        while(index > 0){
            index --;
            cur = cur.next;
        }
        //cur.next = cur.next.next; 
        //cur.next.next.prev = cur; !!!! 错误原因
        cur.next.next.prev = cur; 
        cur.next = cur.next.next;
        size --;
    }
}

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList obj = new MyLinkedList();
 * int param_1 = obj.get(index);
 * obj.addAtHead(val);
 * obj.addAtTail(val);
 * obj.addAtIndex(index,val);
 * obj.deleteAtIndex(index);
 */
