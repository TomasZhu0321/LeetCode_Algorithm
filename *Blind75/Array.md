# 1. Two Sum
* **二刷:11：45(✅)**
* [1. Two Sum](https://leetcode.com/problems/two-sum/)
## 思路1: 双for (自己实现)
* TC: O(N*2)
* SC: O(1)
***
## 思路2: Map记录
### 思路
* While we are iterating, we can use a Map to store the path we've been to. If the result of target - nums[i] exits in the current map, return. Otherwise, insert the nums[i] into the map.
### Code 
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (map.containsKey(complement)) {
                return new int[] { map.get(complement), i };
            }
            map.put(nums[i], i);
        }
        // In case there is no solution, we'll just return null
        return null;
    }
}
```

***
# 121. Best Time to Buy and Sell Stock
* **二刷: 15mins(❌)**
* [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

## 思路1: 记录peaks & valleys (最值)
* TC:O(N)
* SC:O(1)
### 思路
* 通过 low来记录最小值；通过maxProfit来记录最大值结果
* 注意single day是不能又买又卖。因此通过**if - elseif**，如果找到了min就跳过找下一个；如果没找到就比较maxprofit看是不是最大
### Code
```java
class Solution {
    public int maxProfit(int[] prices) {
        int low = Integer.MAX_VALUE;
        int maxProfit = 0;
        for(int i = 0 ; i < prices.length; i ++){
            if(prices[i] < low){
                low = prices[i];
            }else if(prices[i] - low > maxProfit){
                maxProfit = prices[i] - low;
            }
        }
        return maxProfit;
    }
}
```
## 思路2: 二维DP
* TC:O(N)
* SC:O(N)
### 思路
* 二维dp：
  * dp含义：当天买/卖的最值
  * 每天的值都是之前记录中的最大
  * 最后一天就是最大值
### Code
```java
class Solution {
    public int maxProfit(int[] prices) {
        int [][] dp = new int [prices.length][2];
        dp[0][0] = -prices[0];
        for(int i = 1; i < prices.length; i ++){
            //buy (since is negative value, so actually find the mini)
            dp[i][0] = Math.max(-prices[i], dp[i - 1][0]);
            //sell: max profit
            dp[i][1] = Math.max(prices[i] + dp[i - 1][0], dp[i - 1][1]);
        }
        return dp[prices.length - 1][1];
    }
}
```
***
# 217. Contains Duplicate
*  **一刷: 5mins(✅)**
* [217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)

## 考点: Set的underlying implementation & set.add return boolean
* HashSet底层实现是HashMap. set.add返回值是boolean
## Code
* TC: O(N)
* SC: O(N)
```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for(int i : nums){
            if(set.add(i) == false) return true;
            
        }return false;
    }
}
```