# 509. Fibonacci Number
* **一刷:6：45(✅)**
* [509. Fibonacci Number](https://leetcode.com/problems/fibonacci-number/description/)

## My Code
* 思路(递归五部曲)
  * 1\确定'dp'数组+下标含义: `res[i]`存储对应n的 fib数
  * 2\确定'递推'公式: `res[i]=res[i-1] + res[i-2]`
  * 3\dp数组'初始化':`res[0]=0 res[1]=1`
  * 4\ "遍历顺序":从前往后
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
***
# 70. Climbing Stairs
* **一刷:6：45(✅)**
* [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/description/)

## My Code
```java
class Solution {
    public int climbStairs(int n) {
        int [] stairMethods = new int [n];
        stairMethods[0] = 1;
        if(n >= 2){
            stairMethods[1] = 2;
        }
        for(int i = 2; i < stairMethods.length; i ++){
            stairMethods[i] = stairMethods[i-1] + stairMethods[i-2];
        }
        return stairMethods[n-1];
    }
}
```
***
# 746. Min Cost Climbing Stairs
* **一刷:10:10(✅)**
* [746. Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/description/)

## My Code
```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int [] dp = new int [cost.length + 1];
        for(int i = 2; i < dp.length; i ++){
            dp[i] = Math.min(dp[i-1] + cost[i - 1], dp[i-2]+cost[i-2]);
        }
        return dp[dp.length - 1];
    }
}
```