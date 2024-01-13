# 122. Best Time to Buy and Sell Stock II
* **一刷:14:36(✅)**
* [122. Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/)

## My Idea
* 找到上升坡度，也就是分解profit就可以了
```java
class Solution {
    public int maxProfit(int[] prices) {
        int maxProfit = 0;
        for (int i = 1; i < prices.length ; i ++){
            if(prices[i] - prices[i - 1] > 0){
                maxProfit = maxProfit + prices[i] - prices[i - 1];
            }
        }
        return maxProfit;
    }
}
```
***
# 55. Jump Game
* **一刷:40:34(✅)**
* [55. Jump Game](https://leetcode.com/problems/jump-game/)

## My Code
```java
class Solution {
    public boolean canJump(int[] nums) {
        int start = 0;
        int end = 0;
        int tmp = nums[start];
        end = tmp + start;
        if(end >= nums.length - 1){return true;}
        while(start <= end){
            if (nums[start] + start > end){
                end = nums[start] + start;
                if(end >= nums.length - 1){return true;}
            }
            start ++;
            if(start > end) return false;
        }
        return false;
    }
}
```
## 代码随想录Code
```java
class Solution {
    public boolean canJump(int[] nums) {
        if (nums.length == 1) {
            return true;
        }
        //覆盖范围, 初始覆盖范围应该是0，因为下面的迭代是从下标0开始的
        int coverRange = 0;
        //在覆盖范围内更新最大的覆盖范围
        for (int i = 0; i <= coverRange; i++) {
            coverRange = Math.max(coverRange, i + nums[i]);
            if (coverRange >= nums.length - 1) {
                return true;
            }
        }
        return false;
    }
}
```

