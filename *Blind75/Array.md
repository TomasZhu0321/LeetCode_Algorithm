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
***
# 238. Product of Array Except Self
*  **一刷: 25mins(✅)**
* [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)

## 思路1: 从左到右，再从右到左
### 思路：
* 从左到右除开本身先iterate一遍
* 从右到左，通过一个tmp来记录nums[i]，把剩下的补齐
### Code
```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int [] arr = new int [nums.length];
        arr[0] = 1;
        for (int i = 1; i < nums.length ; i ++){
            arr[i] = nums[i - 1] * arr[i - 1];
        }
        int tmp = nums[nums.length - 1];
        for (int i = nums.length - 2; i >= 0 ; i --){
            arr[i] = arr[i] * tmp;
            tmp = tmp * nums[i];
        }
        return arr;
    }
}
```
***
# 53. Maximum Subarray
* **一刷:30:12(✅)**
* [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
## 思路1: 二维DP
### 思路
* DP数组[0]:不取当前值的最大值； DP数组[1]:取当前值的最大值
* dp[i][0]由dp[i - 1]取和不取的最大值得到
* dp[i][1]由取前面和重新开始(只选当前)的最大值得到
### Code
* TC:O(N)
* SC:O(N)
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int [] dp = new int [nums.length + 1];
        int max = Integer.MIN_VALUE;
        for (int i = 1; i <= nums.length; i ++){
            dp[i] = Math.max(dp[i-1]+nums[i - 1],nums[i - 1]);
            max = Math.max(max, dp[i]);
        }
        return max;
    }
}
```
## 思路2: 一维DP，通过一个max来单独记录最大值
* dp[i]: 代表 当前值 以及 之前sum 的最大值
* 通过max来记录最大值可以让dp专注于迭代当前值的最优情况(哪怕前面出现了最优结果，也没关系)
* 通过dp[i]表达式来确定如何初始化数组
### Code
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int max = Integer.MIN_VALUE;
        int [] dp = new int [nums.length + 1];
        for(int i = 1; i <= nums.length ; i ++){
            dp[i] = Math.max(dp[i - 1] + nums[i - 1], nums[i - 1]);
            max = Math.max(dp[i],max);
        }
        return max;
    }
}
```
## 思路3: **Kadane's Algorithm** 
* 解决**Maximum subarry 问题**的一种高效算法
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int max_so_far = nums[0];
        int result = nums[0];
        for(int i = 1; i < nums.length ; i ++){
            max_so_far = Math.max(max_so_far + nums[i], nums[i]);
            result = Math.max(result,max_so_far);
        }
        return result;
    }
}
```

***
# 152. Maximum Product Subarray
* **一刷:30:12(❌)**
* [152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)

## 思路1: Kadane算法
* 问题的点在于negative value会导致结果彻底反转
  * 通过记录一个**min_so_far**
* 遇到0会彻底失效
  * 在`Math.min(nums[i],Math.min(num[i]*min_so_far , min[i]*max_so_far))`;中, `num[i]`就相当于本身`x1`了
### Code
```java
class Solution {
    public int maxProduct(int[] nums) {
        double result = nums[0];
        double max_so_far = nums[0];
        double min_so_far = nums[0];
        for(int i = 1; i < nums.length; i ++){
            double tmp_max = Math.max(nums[i],Math.max(min_so_far * nums[i],max_so_far * nums[i]));
            System.out.println(i + " - Max: " + tmp_max);
            min_so_far = Math.min(nums[i],Math.min(max_so_far * nums[i],min_so_far * nums[i]));
            System.out.println(i + " - Min: "  + min_so_far);
            max_so_far = tmp_max;
            result = Math.max(result, max_so_far);
        }
        return (int)result;
    }
}
```
***

# 153. Find Minimum in Rotated Sorted Array
* [153. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

## 思路1: Binary Search
* Binary Search最容易错的是 **termination point**
  * 本题当mid的值等于left或者right，说明了范围就在两个当中
  * 去两个当中最小的就是答案
### Code
```java
class Solution {
    public int findMin(int[] nums) {
        int left = 0;
        int right = nums.length - 1;
        if (nums[left] < nums[right] ) return nums[left];
        int mid = ( right - left ) / 2;
        while(left < right){
            mid = left + ( right - left ) / 2;
            if(mid == left || mid == right){
                if(mid == left) return Math.min(nums[mid + 1], nums[mid]);
                else return Math.min(nums[mid - 1], nums[mid]);
            }
            if(nums[mid] < nums[right] && nums[left] > nums[right]){
                right = mid;               
            }
            else if(nums[mid] > nums[right] && nums[left] > nums[right]){
                left = mid;               
            }
            
        }
        return nums[mid];
    }
}
```