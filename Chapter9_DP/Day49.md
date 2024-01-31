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

# 122. Best Time to Buy and Sell Stock II
* **一刷:16:50(✅)**
* [122. Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/)

## My Code
* 思路：注意的是当天买入的状态可以是卖了前一天的，再买当天的，因为同一天可以两个操作
  * `dp[i][1]`需要在之前

```java
class Solution {
    public int maxProfit(int[] prices) {
        int [][] dp = new int [prices.length][2];
        dp[0][0] = -prices[0];
        for(int i = 1; i < prices.length; i ++){
            dp[i][1] = Math.max(dp[i - 1][1], dp[i - 1][0] + prices[i]);
            dp[i][0] = Math.max(dp[i][1]-prices[i], dp[i - 1][1] - prices[i]);
        }
        return Math.max(dp[prices.length - 1][0], dp[prices.length - 1][1]);
    }
}
```
## Improvement
* 其实dp[i-1][0]的状态就代表了卖出再买入的状态
```java
for(int i = 1; i < prices.length; i ++)
{
    dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1] - prices[i]);
    dp[i][1] = Math.max(dp[i - 1][1], dp[i - 1][0] + prices[i]);
}
```