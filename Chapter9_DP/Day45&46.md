# 322. Coin Change
* **一刷:17:43(✅)**
* [322. Coin Change](https://leetcode.com/problems/coin-change/)
## My Code
* 注意在条件判断的时候，还要判断`dp[i - coins[j]]!=Integer.MAX_VALUE`
```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        int [] dp = new int [amount + 1];
        for (int i = 1; i < dp.length ; i ++){
            dp[i] = Integer.MAX_VALUE;
        }
        for (int i = 0 ; i < amount + 1; i ++){
            for (int j = 0 ; j < coins.length; j ++){
                if(i - coins[j] >= 0 && dp[i - coins[j]]!=Integer.MAX_VALUE){
                    dp[i] = Math.min(dp[i - coins[j]] + 1, dp[i]);
                }
            }
        }
        return dp[amount] == Integer.MAX_VALUE ? -1: dp[amount];
    }
}
```

***
# 279. Perfect Squares
* **一刷:12:34(✅)**
* [279. Perfect Squares](https://leetcode.com/problems/perfect-squares/description/)

## My Code
```java
class Solution {
    public int numSquares(int n) {
        int nums = Math.round((int)Math.sqrt(n));
        int [] values = new int [nums];
        for (int i = 0; i < values.length; i ++){
            values[i] = (i+1)*(i+1);
        }
        int [] dp = new int [n + 1];
        for(int i = 1; i < dp.length; i++){
            dp[i] = Integer.MAX_VALUE;
        }
        for (int i = 0; i < dp.length; i ++){
            for (int j = 0; j < values.length; j ++){
                if(i - values[j] >= 0 && dp[i - values[j]]!= Integer.MAX_VALUE){
                    dp[i] = Math.min(dp[i - values[j]] + 1, dp[i]);
                }
            }
        }
    return dp[n];
    }
}
```

## Improvement
* 不用创建一个新的数组`values[]`来存放 `n*n`,作为遍历的内容 ==>直接 `int i = 1; i * i <= n` 作为物品的遍历
* 不用 每次都从0开始一次遍历，只用跳到`i*i`的地方就可以了，因为其他地方对结果没有影响

```java
class Solution {
    public int numSquares(int n) {
        int max = Integer.MAX_VALUE;
        int[] dp = new int[n + 1];
        //初始化
        for (int j = 0; j <= n; j++) {
            dp[j] = max;
        }
	//如果不想要寫for-loop填充數組的話，也可以用JAVA內建的Arrays.fill()函數。
	//Arrays.fill(dp, Integer.MAX_VALUE);
	
        //当和为0时，组合的个数为0
        dp[0] = 0;
        // 遍历物品
        for (int i = 1; i * i <= n; i++) {
            // 遍历背包
            for (int j = i * i; j <= n; j++) {
                //if (dp[j - i * i] != max) {
                    dp[j] = Math.min(dp[j], dp[j - i * i] + 1);
                //}
		//不需要這個if statement，因爲在完全平方數這一題不會有"湊不成"的狀況發生（ 一定可以用"1"來組成任何一個n），故comment掉這個if statement。
            }
        }
        return dp[n];
    }
}
```
# 139. Word Break
* **一刷:36:51(✅)**
* [139. Word Break](https://leetcode.com/problems/word-break/description/)
## My Code
```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        boolean [] dp = new boolean [s.length() + 1];
        dp[0] = true;
        for(int i = 0; i < s.length() + 1; i ++){
            for(String str : wordDict){
                int len = str.length();
                if(i >= len && dp[i - len] && s.substring(i - len ,i).equals(str)){
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[s.length()];
    }
}
```
