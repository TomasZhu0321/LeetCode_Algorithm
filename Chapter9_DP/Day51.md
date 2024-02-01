# 309. Best Time to Buy and Sell Stock with Cooldown
* **一刷:60:50(❌)**
* [309. Best Time to Buy and Sell Stock with Cooldown](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

## Question
### 没有理清状态，以及之间的关系

## 思路
![image](https://github.com/TomasZhu0321/LeetCode_Algorithm/blob/main/Chapter9_DP/img/309_1.jpg)
![image](https://github.com/TomasZhu0321/LeetCode_Algorithm/blob/main/Chapter9_DP/img/309_2.jpg)

## Code
```java
class Solution {
    public int maxProfit(int[] prices) {
        int len = prices.length;
        if (len == 1) return 0;
        int [] dp = new int [4];
        dp[0] = -prices[0];
        for(int i = 1; i < len; i ++){
            //hold stock
            int zero = Math.max(Math.max(dp[3] - prices[i], dp[0]),dp[2] - prices[i]);
            //sell stock 
            int one  = dp[0] + prices[i];
            //cooldown
            int two  = dp[1];
            //keep sold status
            int three = Math.max(dp[2], dp[3]);
            dp[0] = zero;
            dp[1] = one;
            dp[2] = two;
            dp[3] = three;
        }
        int max = Math.max(dp[0],dp[1]);
        int max2 = Math.max(dp[2],dp[3]);
        return Math.max(max,max2);
    }
}
```
