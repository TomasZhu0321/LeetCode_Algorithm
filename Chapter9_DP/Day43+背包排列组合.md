# 1049. Last Stone Weight II
* **一刷:19:04(✅)**
* [1049. Last Stone Weight II](https://leetcode.com/problems/last-stone-weight-ii/description/)

## My Code
* 思路: 抽象成两个差不多的石头相撞，这样的结果就最小
  * 将total分成一半一半作为dp背包的容积
  * 遍历的最后结果就是其中一半最大能达到的重量
```java
class Solution {
    public int lastStoneWeightII(int[] stones) {
        int total = 0;
        for(int i : stones){
            total += i;
        }
        int half = total>>1;
        int [][] dp = new int [stones.length][half + 1];
        for (int j = 0; j < half + 1; j ++){
            if(j >= stones[0]){
            dp[0][j] = stones[0];
        }
        }
        for (int i = 1; i < stones.length; i ++){
            for (int j = 1; j < half + 1; j ++){
                if(j >= stones[i]){
                    dp[i][j] = Math.max(dp[i - 1][j - stones[i]] + stones[i], dp[i - 1][j]);
                }
                else {
                    dp[i][j] = dp[i - 1][j];
                }
            }
        }
        int res = dp[stones.length - 1 ][half];
        return total - res - res;
    }
}
```
# 494. Target Sum
* **一刷:60(❌)**
* [494. Target Sum](https://leetcode.com/problems/target-sum/)
## 反思
* **First Obstacle**: 不知道"背包"代表的含义
  * 通过公式推导出`bag = ( target + sum )/2;` dp[]的含义是 在  `nums[i] 的情况下, 装满 j 的可能性 `
* **Second Obstacle**: 未考虑如果为0 的情况。二维数组需要将0的情况单独领出来，因为是从`i = 1, j = 1` 开始遍历的
  * 因为0可以+可以-,所以遍历0的个数，最后`0的结果是2^n`
```java
//错误代码
class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        int total = 0;
         for(int i : nums){
            total += Math.abs(i);
         }
        
        int cap = (total + Math.abs(target))>>1;
        if((total + Math.abs(target))%2 == 1) return 0;
        int [][] dp = new int [nums.length][cap + 1];
        for (int i = 0; i < cap + 1; i ++){
            if(i == nums[0]){
                dp[0][i] = 1;
            }
        }
        for(int i = 1; i < nums.length; i ++){
            for (int j = 0; j < cap + 1; j ++){
                int tmp = 0;
                if(j == Math.abs(nums[i])){
                    tmp = 1;
                }
                if(j - Math.abs(nums[i]) >= 0){
                        dp[i][j] = dp[i - 1][j - Math.abs(nums[i])] + dp[i-1][j] + tmp;
                    }
                }
        }
        return dp[nums.length - 1][cap];
    }
}

//正确代码：二维数组

class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        int total = 0;
         for(int i : nums){
            total += Math.abs(i);
         }
        
        int cap = (total + Math.abs(target))>>1;
        if((total + Math.abs(target))%2 == 1) return 0;
        int [][] dp = new int [nums.length][cap + 1];
        for (int i = 0; i < cap + 1; i ++){
            if(i == nums[0]){
                dp[0][i] = 1;
            }
        }
        int numZeros = 0;
        for(int i = 0; i < nums.length; i++) {
            if(nums[i] == 0) {
                numZeros++;
            }
            dp[i][0] = (int) Math.pow(2, numZeros);
        }
        for(int i = 1; i < nums.length; i ++){
            for (int j = 1; j < cap + 1; j ++){
                if(j - Math.abs(nums[i]) >= 0){
                        dp[i][j] = dp[i - 1][j - Math.abs(nums[i])] + dp[i-1][j];
                }
                else {
                    dp[i][j] = dp[i-1][j];
                }
        }
        }
        return dp[nums.length - 1][cap];
    }
}
```
### ❗️" 排列组合问题 "考虑使用一维数组
* 遍历顺序: nums[i] ==> 背包
* 初始化: dp[0] = 1; //理解: 背包的内容相当于是排列组合的个数，那么dp[0]就是什么也不装,也是0， 所以dp[0] = 1;
```java
class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        int sum = 0;
        for (int i = 0; i < nums.length; i++) sum += Math.abs(nums[i]);

        if ((Math.abs(target) + sum) % 2 == 1) return 0;

        int bagSize = (Math.abs(target) + sum) / 2;
        int[] dp = new int[bagSize + 1];
        dp[0] = 1;
        for (int i = 0; i < nums.length; i++) {
            for (int j = bagSize; j >= Math.abs(nums[i]); j--) {
                dp[j] += dp[j - Math.abs(nums[i])];
            }
        }
        return dp[bagSize];
    }
}
```
