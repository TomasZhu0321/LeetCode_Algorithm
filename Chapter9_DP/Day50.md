# 123. Best Time to Buy and Sell Stock III
* **一刷:60:02(❌)**
* [123. Best Time to Buy and Sell Stock III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/description/)
* 代码随想录:[123题解](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0123.%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%BAIII.md)
## Questions
![image](https://github.com/TomasZhu0321/LeetCode_Algorithm/blob/main/Chapter9_DP/img/123.jpg)
### Q1. 如何将trans 1和2分开？何时启动 trans2?
* 这里不用分开。而是通过dp[4]的数组，记录了`买1卖1买2卖2`的状态，并将最终的最大状态`滚动到了dp[3]`
### Q2. 自己思路1: 找最值 => 会错过两个小高峰 e.g.[3,3,5,0,0,3,1,4]
### Q3. 自己思路2: 找累计增量 => 会损失横跨 e.g. [1,2,3,4,5]
* 通过dp数组，每次都是记录手上最大的财富。每天可以进行的交易量是不限的，也就是当天可以`买卖再买再卖`
* 注意看`买2`也就是`dp[2]`，这里是通过`dp[1]来计算的当前财富`，也就是进行了划分。因为dp[1]代表的第一次卖出

## Code
```java
class Solution {
    public int maxProfit(int[] prices) {
        int len = prices.length;
        if(len == 1){
            return 0;
        }
        int [] dp = new int [4];
        dp[0] = -prices[0];
        dp[2] = -prices[0];
        for(int i = 1; i < len; i ++){
            int zero = Math.max(-prices[i],dp[0]);
            int one = Math.max(prices[i] + dp[0], dp[1]);
            int two = Math.max( dp[1]-prices[i] , dp[2]);
            int three = Math.max(dp[2] + prices[i],dp[3]);
            dp[0] = zero;
            dp[1]= one;
            dp[2] = two;
            dp[3] = three;
        }
        return dp[3];
    }
}
```
