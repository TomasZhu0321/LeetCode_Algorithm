# 225. Implement Stack using Queues
* **一刷:16：04(✅)**
* [225. Implement Stack using Queues](https://leetcode.com/problems/implement-stack-using-queues/)

## My Code
```java
class MyStack {
    int size;
    Deque<Integer> dq;

    public MyStack() {
        size = 0;
        dq = new LinkedList<>();
    }

    public void push(int x) {
        dq.offer(x);
        size++;
        int time = size - 1;
        while (time != 0) {
            dq.offer(dq.poll());
            time--;
        }
    }

    public int pop() {
        size--;
        return dq.poll();
    }

    public int top() {
        return dq.peek();
    }

    public boolean empty() {
        if (size == 0)
            return true;
        return false;
    }
}
```