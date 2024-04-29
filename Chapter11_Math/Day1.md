# 9. Palindrome Number
* **一刷:10:02(✅)**
* [9. Palindrome Number](https://leetcode.com/problems/palindrome-number/?envType=study-plan-v2&envId=top-interview-150)

## My Code
```java
class Solution {
    public boolean isPalindrome(int x) {
        if(x < 0) return false;
        Deque <Integer> que = new LinkedList<>();
        int n = x % 10;
        int m = x / 10;
        que.offer(n);
        while(m != 0){
            n = m % 10;
            m = m / 10;
            que.offer(n);
        }
        while(!que.isEmpty()){
            if(que.size() == 1)return true;
            if(que.size() > 1 && que.getLast() == que.peek()){
                que.pollLast();
                que.poll();
            }else {
                return false;
            }
        }
        return true;
    }
}
```