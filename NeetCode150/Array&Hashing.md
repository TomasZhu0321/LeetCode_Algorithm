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
* **一刷:28:12(✅)**
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
# 33. Search in Rotated Sorted Array
* **一刷:50：45(❌)**
* [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)

## 思路1: 二分法，找准一定有一边是sorted
* 本题的破题点是: 二分法后，一定有一边是sorted的！
* 那么先通过`if nums[left] <= nums[mid]`来将其分割成两部分，一部分有序，一部分无序。如果不在当前范围内，直接在另一半中去找
### Code
```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        int mid = left + (right - left) / 2;
        while (left <= right) {
            mid = left + (right - left) / 2;
            if (nums[mid] == target)
                return mid;
            //sorted order
            if(nums[left] <= nums[mid]){
                if(target < nums[mid] && target >= nums[left]){
                    right = mid - 1;
                }else {
                    left = mid + 1;
                }
            }else {
                if(target <= nums[right] && target > nums[mid]){
                    left = mid + 1;
                }else {
                    right = mid - 1;
                }
            }
        }
        return -1;
    }
}
```
# 15. 3Sum
* **二刷:40:32(❌)**
* [15. 3Sum](https://leetcode.com/problems/3sum/)
## 分析
![image](img/15.jpg)
### 思路
* 通过`双指针`，控制i为最外收束的，left通过i的值来确定==>`left = i + 1`
* **去重**: 去重逻辑不光需要考虑i的去重，`left和right也需要`(自己考虑到！) 


## My Code
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> res = new LinkedList<>();
        for(int i = 0; i <= nums.length - 2; i ++){
            if(i > 0 && nums[i - 1] == nums[i]) continue;
            int left = i + 1;
            int right = nums.length - 1;
            while(left < right){
                int tmpRes = nums[i] + nums[left] + nums[right];
                if(tmpRes < 0) left ++;
                else if(tmpRes > 0) right --;
                else {
                    List<Integer> r = new LinkedList<>();
                    r.add(nums[i]);
                    r.add(nums[left]);
                    r.add(nums[right]);
                    res.add(r);
                    while (right > left && nums[right] == nums[right - 1]) right--;
                    while (right > left && nums[left] == nums[left + 1]) left++;  
                    right--; 
                    left++;
                }
            }
        }
        return res;
    }
}
```
***
# 11. Container With Most Water
* **一刷:15:32(❌)**
* [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
## 思路1: 双指针
* left和right的移动是: 哪边的柱子低一点，就移动哪一边
```java
class Solution {
    public int maxArea(int[] height) {
        int left = 0;
        int right = height.length - 1;
        int max = Integer.MIN_VALUE;
        while(left < right){
            int water = (right - left) * (Math.min(height[left],height[right]));
            max = Math.max(max,water);
            if(height[left] <= height[right]){
                left ++;
            }else {
                right --;
            }
        }
        return max;
    }
}
```
***
# 36. Valid Sudoku
* **一刷:36:32(❌)**
* [36. Valid Sudoku](https://leetcode.com/problems/valid-sudoku/)
## 思路1: `Map<Integer, HashSet<Character>> `
### 知识点
* 可以通过`Map + Set`的方式，map来记录区域，set来记录每个区域的使用情况: `Map<Integer, HashSet<Character>> row = new HashMap<>();`
* `map.getOrDefault(row, new HashSet<>())` : 如果不存在返回new HashSet<>()，但不会插入进map中
* `map.computeIfAbsent(row, k -> new HashSet<>())` : 如果不存在，创建新的HashSet,并且插入进map中（如果存在就返回key对应的value
* getOrDefault和computeIfAbsent的区别就是一个会改变(computeIfAbsent)map的mapping一个不改变(getOrDefualt)

### Code 
```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        Map<Integer, HashSet<Character>> row = new HashMap<>();
        Map<Integer, HashSet<Character>> col = new HashMap<>();
        Map<Integer, HashSet<Character>> square = new HashMap<>();
        for(int i = 0;i<9;i++){
            for(int j = 0; j < 9; j++){
                char c = board[i][j];
                if(c == '.'){
                    continue;
                }
                if(row.getOrDefault(i,new HashSet<>()).contains(c)||
                col.getOrDefault(j,new HashSet<>()).contains(c) ||
                square.getOrDefault((i/3)*3 + j/3, new HashSet<>()).contains(c)){
                    return false;
                }
                row.computeIfAbsent(i, k -> new HashSet<>()).add(c);
                col.computeIfAbsent(j, k->new HashSet<>()).add(c);
                square.computeIfAbsent( (i/3)*3 + j/3, k->new HashSet<>()).add(c);
                
            }
        }
        return true;
        
    }
}
```