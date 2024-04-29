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
***
# 66. Plus One
* **一刷:15:02(✅)**
* [66. Plus One](https://leetcode.com/problems/plus-one/?envType=study-plan-v2&envId=top-interview-150)

## My Code
```java
class Solution {
    public int[] plusOne(int[] digits) {
        if (digits[digits.length - 1] != 9) {
            digits[digits.length - 1]++;
            return digits;
        }
        Deque<Integer> dq = new LinkedList<>();
        boolean flag = true;
        for(int i = digits.length - 1; i >=0 ; i --){
            if(flag && digits[i] == 9){
                dq.offer(0);
                if(i == 0){
                    dq.offer(1);
                }
                continue;
            }
            if (flag && digits[i] != 9){
                dq.offer(digits[i] + 1);
                flag = false;
                continue;
            }
            if(!flag){
                dq.offer(digits[i]);
                continue;
            }
        }
        int [] res = new int [dq.size()];
        for(int i = 0 ; i < res.length; i ++){
            res[i] = dq.pollLast();
        }
        return res;
    }
}
```