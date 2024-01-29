# 完全背包🎒
* 每个商品`无限个`
* 和`0-1背包`的主要区别是:**遍历顺序**
  * 一维数组的完全背包: `物品`和`背包容量`都是从`小 -->大`去遍历 (因为之前从大到小是为了不重复的取，而完全背包就是让你重复的取)

```java
//先遍历物品，再遍历背包
private static void testCompletePack(){
    int[] weight = {1, 3, 4};
    int[] value = {15, 20, 30};
    int bagWeight = 4;
    int[] dp = new int[bagWeight + 1];
    for (int i = 0; i < weight.length; i++){ // 遍历物品
        for (int j = weight[i]; j <= bagWeight; j++){ // 遍历背包容量
            dp[j] = Math.max(dp[j], dp[j - weight[i]] + value[i]);
        }
    }
    for (int maxValue : dp){
        System.out.println(maxValue + "   ");
    }
}
```

# 518. Coin Change II
* **一刷:14:04(✅)**
* [518. Coin Change II](https://leetcode.com/problems/coin-change-ii/)

```java
class Solution {
    public int change(int amount, int[] coins) {
        int [] dp = new int [amount + 1];
        dp[0] = 1;
        for (int i = 0; i < coins.length; i ++){
            for (int j = 0; j <= amount; j ++){
                if(j >= coins[i]){
                    dp[j] = dp[j - coins[i]] + dp[j];
                }
            }
        }
        return dp[amount];
    }
}
```

# 377. Combination Sum IV
* **一刷:26:43(✅)**
* [377. Combination Sum IV](https://leetcode.com/problems/combination-sum-iv/)

## My Code
```java
class Solution {
    public int combinationSum4(int[] nums, int target) {
        int [] dp = new int [target + 1];
        dp[0] = 1;
        for (int i = 0; i < target + 1 ; i ++){
            for (int j = 0; j < nums.length; j ++){
                if(i - nums[j] >= 0){
                    dp[i] += dp[i - nums[j]];
                }
            }
        }
        return dp[target];
    }
}
```