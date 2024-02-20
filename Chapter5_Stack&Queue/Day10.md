# 232. Implement Queue using Stacks
* **一刷:17：04(✅)**
* [232. Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/)

## My Code
```java
class MyQueue {
    Stack <Integer> stack1;
    Stack <Integer> stack2;
    int size ;
    public MyQueue() {
        stack1 = new Stack<>();
        stack2 = new Stack<>();
        size = 0;
    }
    
    public void push(int x) {
        while(!stack2.isEmpty()){
            int tmp = stack2.pop();
            stack1.push(tmp);
        }
        stack1.push(x);
        size ++;
    }
    
    public int pop() {
        while(!stack1.isEmpty()){
            int tmp = stack1.pop();
            stack2.push(tmp);
        }
        size --;
        return stack2.pop();
    }
    
    public int peek() {
         while(!stack1.isEmpty()){
            int tmp = stack1.pop();
            stack2.push(tmp);
        }
        return stack2.peek();
    }
    
    public boolean empty() {
        return size == 0 ? true : false;
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
```
