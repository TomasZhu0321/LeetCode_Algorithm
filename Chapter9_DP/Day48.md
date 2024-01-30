# 198. House Robber
* **一刷:16:42(✅)**
* [198. House Robber](https://leetcode.com/problems/house-robber/)

## My Code
* 思路
  * 通过二维数组记录每次买或者不买的最高价格
```java
class Solution {
    public int rob(int[] nums) {
        int [][] dp = new int[nums.length][2];
        dp[0][1] = nums[0];
        for(int i = 1; i < nums.length; i ++){
            //do not rob current one
            dp[i][0] = Math.max(dp[i - 1][0],dp[i - 1][1]);
            //rob current one
            if(i == 1){
                dp[i][1] = nums[i];
            }
            if(i >= 2){
                dp[i][1] = Math.max(dp[i-2][0],dp[i-2][1]) + nums[i];
            }
            
        }
        return Math.max(dp[nums.length - 1][0],dp[nums.length - 1][1]);
    }
}
```

## Improvement 
* 通过滚动数组，只用`int [] dp = new int [2]`来记录 `前一次 dp[1]` 和 `前两次 dp[0]`的最高纪录
* 精妙的点在于他的dp是记录的 `n-1` 和 `n-2` 结果的最高值，每次往前走一步,`n-1 ==> n-2`
```java
class Solution {
    public int rob(int[] nums) {
        if(nums.length == 1){
            return nums[0];
        }
        int [] dp = new int [2];
        dp[0] = nums[0];
        dp[1] = Math.max(nums[0],nums[1]);
        int res = 0;
        for (int i = 2; i < nums.length; i ++){
            res = Math.max(dp[0] + nums[i], dp[1]);
            dp[0] = dp[1];
            dp[1] = res;
        }
        return dp[1];
    }
}
```

