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
***
# 213. House Robber II
* **一刷:47:49(✅)**
* [213. House Robber II](https://leetcode.com/problems/house-robber-ii/description/)

## My Code
* 思路:
  * 通过构建一个二维数组。row 1表示以0开头/ row 2表示以 1 开头
  * 类似两个交错开的龙头，用来模拟最后一个 的情况
  * 注意的是第一个和最后一个的初始值和结束条件不一样

```java
class Solution {
    public int rob(int[] nums) {
        if(nums.length == 1){
            return nums[0];
        }
        if(nums.length == 2){
            return Math.max(nums[0],nums[1]);
        }
        int [][] dp = new int [2][2];
        dp[0][0] = nums[0];
        dp[0][1] = Math.max(nums[0],nums[1]);
        if(nums.length >= 2){
        dp[1][0] = 0;
        dp[1][1] = nums[1];
        }
        if(nums.length >= 3){
            for(int i = 2; i < nums.length; i ++){
            if(i < nums.length - 1){
                int tmp0 = Math.max(dp[0][0] + nums[i], dp[0][1]);
                dp[0][0] = dp[0][1];
                dp[0][1] = tmp0;
            }
            if(i == 2){
                dp[1][0] = nums[1];
                dp[1][1] = Math.max(nums[2],nums[1]);
                continue;
            }
            int tmp1 = Math.max(dp[1][0] + nums[i], dp[1][1]);
            dp[1][0] = dp[1][1];
            dp[1][1] = tmp1;
            }
        }
        return Math.max(dp[1][1],dp[0][1]);
    }
}
```
***
# 337. House Robber III
* **一刷:30:30(❌)**
* [337. House Robber III](https://leetcode.com/problems/house-robber-iii/)

## 问题
### Q1: 知道是 post-order，但是如何区分 左右/中？
![image](https://github.com/TomasZhu0321/LeetCode_Algorithm/blob/main/Chapter9_DP/img/337.png)
### Q2: dp记录的是什么，如何与post-order 递归相结合

## 解决
* 先确定`递归`的逻辑: 左右中。然后返回值🔙应该是dp数组，dp[2];记录了`偷当前值`和`不偷当前值`
* `dp[0] = 左孩子的最大 + 右孩子的最大`
* `dp[1] = 不偷左孩子结果 + 不偷右孩子结果 + 中`
* 难点在于没有想到数组的迭代

```java
class Solution {
    public int rob(TreeNode root) {
        int [] res = robAction (root);
        return Math.max(res[0],res[1]);
    }
    private int [] robAction(TreeNode root){
        int [] dp = new int [2];
        if(root == null){
            return dp;
        }
        int [] left = robAction(root.left);
        int [] right = robAction(root.right);
        dp[0] = Math.max(left[0],left[1]) + Math.max(right[0],right[1]);
        dp[1] = left[0] + right[0] + root.val;
        return dp;
    }
}
```

