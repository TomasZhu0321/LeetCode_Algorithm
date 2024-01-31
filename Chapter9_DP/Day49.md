# 121. Best Time to Buy and Sell Stock
* **一刷:20:02(✅)**
* [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)


## My Code
* 注意题目说的`只能买一次，只能卖一次`，因此是找最值
```java
class Solution {
    public int maxProfit(int[] prices) {
        int [][] dp = new int [prices.length][2];
        dp[0][0] = -prices[0];
        for (int i = 1 ; i < prices.length; i ++){
            dp[i][0] = Math.max(-prices[i], dp[i - 1][0]);
            dp[i][1] = Math.max(prices[i] + dp[i - 1][0], dp[i-1][1]);
        }
        return dp[prices.length - 1][1];
    }
}
```