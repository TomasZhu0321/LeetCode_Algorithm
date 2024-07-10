# 70. Climbing Stairs
* **一刷:6：45(✅)**
* [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/description/)

## My Code
```java
class Solution {
    public int climbStairs(int n) {
        if (n == 1) return 1;
        if (n == 2 ) return 2;
        int [] dp = new int [n + 1];
        dp[1] = 1;
        dp[2] = 2;
        for(int i = 3; i <= n; i ++){
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
}
```
***
# 322. Coin Change
* **一刷:36：45(❌)**
* [322. Coin Change](https://leetcode.com/problems/coin-change/)

## 思路1: DP
* 通过一维DP，将amount拆分成一个一个依次累加。每个dp[i]代表的就是当前amount下最小的个数，然后最终的也一定是最小的
* 两个for循环，一个iterate amount，一个iterate coins
* 时间复杂度: O(S * n);
* 空间复杂度: O(S);
### Code  
```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        int [] dp = new int [amount + 1];
        int max = amount + 1;
        Arrays.fill(dp, max);
        dp[0] = 0;
        for(int i = 1; i <= amount; i ++){
            for(int j = 0; j < coins.length; j ++){
                if(coins[j]<=i){
                    dp[i] = Math.min(dp[i], dp[i - coins[j]] + 1);
                }
            }
        }
        return dp[amount] == max ? -1 : dp[amount];
    }
}
```