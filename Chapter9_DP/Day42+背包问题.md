![image](https://github.com/TomasZhu0321/LeetCode_Algorithm/blob/main/Chapter9_DP/img/背包问题1.jpg)

## 法1: 对应代码
```java
public class BagProblem {
    public static void main(String[] args) {
        int[] weight = {1,3,4};
        int[] value = {15,20,30};
        int bagSize = 4;
        testWeightBagProblem(weight,value,bagSize);
    }

    /**
     * 动态规划获得结果
     * @param weight  物品的重量
     * @param value   物品的价值
     * @param bagSize 背包的容量
     */
    public static void testWeightBagProblem(int[] weight, int[] value, int bagSize){

        // 创建dp数组
        int goods = weight.length;  // 获取物品的数量
        int[][] dp = new int[goods][bagSize + 1];

        // 初始化dp数组
        // 创建数组后，其中默认的值就是0
        for (int j = weight[0]; j <= bagSize; j++) {
            dp[0][j] = value[0];
        }

        // 填充dp数组
        for (int i = 1; i < weight.length; i++) {
            for (int j = 1; j <= bagSize; j++) {
                if (j < weight[i]) {
                    /**
                     * 当前背包的容量都没有当前物品i大的时候，是不放物品i的
                     * 那么前i-1个物品能放下的最大价值就是当前情况的最大价值
                     */
                    dp[i][j] = dp[i-1][j];
                } else {
                    /**
                     * 当前背包的容量可以放下物品i
                     * 那么此时分两种情况：
                     *    1、不放物品i
                     *    2、放物品i
                     * 比较这两种情况下，哪种背包中物品的最大价值最大
                     */
                    dp[i][j] = Math.max(dp[i-1][j] , dp[i-1][j-weight[i]] + value[i]);
                }
            }
        }

        // 打印dp数组
        for (int i = 0; i < goods; i++) {
            for (int j = 0; j <= bagSize; j++) {
                System.out.print(dp[i][j] + "\t");
            }
            System.out.println("\n");
        }
    }
}
```
***
![image](https://github.com/TomasZhu0321/LeetCode_Algorithm/blob/main/Chapter9_DP/img/背包2.jpeg)
```java
    public static void main(String[] args) {
        int[] weight = {1, 3, 4};
        int[] value = {15, 20, 30};
        int bagWight = 4;
        testWeightBagProblem(weight, value, bagWight);
    }

    public static void testWeightBagProblem(int[] weight, int[] value, int bagWeight){
        int wLen = weight.length;
        //定义dp数组：dp[j]表示背包容量为j时，能获得的最大价值
        int[] dp = new int[bagWeight + 1];
        //遍历顺序：先遍历物品，再遍历背包容量
        for (int i = 0; i < wLen; i++){
            for (int j = bagWeight; j >= weight[i]; j--){
                dp[j] = Math.max(dp[j], dp[j - weight[i]] + value[i]);
            }
        }
        //打印dp数组
        for (int j = 0; j <= bagWeight; j++){
            System.out.print(dp[j] + " ");
        }
    }
```
# 416. Partition Equal Subset Sum
* **一刷:58:50(✅)**
* [416. Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/description/)

## My Code
* 背包的体积为sum / 2
* 背包要放入的商品（集合里的元素）重量为 元素的数值，价值也为元素的数值
* 背包如果正好装满，说明找到了总和为 sum / 2 的子集
* 背包中每一个元素是不可重复放入
```java
class Solution {
    public boolean canPartition(int[] nums) {
        int total = 0;
        for(int i : nums){
            total += i;
        }
        if(total % 2 == 1) return false;
        int max = total >> 1;
        int [][] dp = new int [nums.length][max + 1];
        for(int i = 1; i <= max; i ++){
            if(nums[0]>= i){
                dp[0][i] = nums[0];
            }
        }
        for (int i = 1; i < nums.length; i ++){
            for (int j = 1; j <= max ; j ++){
                if(nums[i] <= j){
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i - 1][j-nums[i]] + nums[i]);
                }
                else {
                    dp[i][j] = dp[i - 1][j];
                }
                while(dp[i][j] == max )return true;
            }
        }
        return false;
    }
}