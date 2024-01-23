# 509. Fibonacci Number
* **一刷:6：45(✅)**
* [509. Fibonacci Number](https://leetcode.com/problems/fibonacci-number/description/)

## My Code
* 思路(递归五部曲)
  * 1\确定'dp'数组+下标含义: `res[i]`存储对应n的 fib数
  * 2\确定'递推'公式: `res[i]=res[i-1] + res[i-2]`
  * 3\dp数组'初始化':`res[0]=0 res[1]=1`
  * 4\"遍历顺序":从前往后
  * 5\举例
```java
class Solution {
    public int fib(int n) {
        int [] res = new int[n + 1];
        if(n >= 1){
            res[1] = 1;
        }
        for(int i = 2; i < res.length; i ++){
            res[i] = res[i-1]+res[i-2];
        }
        return res[n];
    }
}
```