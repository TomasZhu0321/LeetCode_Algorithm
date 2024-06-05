# 528. Random Pick with Weight
* **一刷:20：45(❌)**
* [528. Random Pick with Weight](https://leetcode.com/problems/random-pick-with-weight/)

## 知识点
### 前缀和prefixSums
* 用处：可以快速计算出i在 它以及他之前的权重。**加权随机选择问题**中，前缀和数组有助于快速找到随机数落在哪个权重区间内.
* 结合**二分法**，能够实现按权重选取随机数

## Code
```java
class Solution {
    int [] preArr;
    int totalSum = 0;
    Random rand;
    public Solution(int[] w) {
        preArr = new int [w.length];
        int index = 0 ;
        for(int i : w){
            totalSum += i;
            preArr[index] = totalSum;
            index ++;
        }
        rand = new Random();
    }
    
    public int pickIndex() {
        int r = rand.nextInt(totalSum);
        int start = 0;
        int end = preArr.length - 1;
        while(start < end){
            int mid = start + (end - start)/2;
            if (preArr[mid] <= r){
                start = mid + 1;
            }
            else{
                end = mid;
            }
        }
        return end;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(w);
 * int param_1 = obj.pickIndex();
 */
```
***
# 1060. Missing Element in Sorted Array
* **一刷:20：45(❌)**
* [1060. Missing Element in Sorted Array](https://leetcode.com/problems/missing-element-in-sorted-array/)

## 思路
* 可以通过index之间的差值来确定missing values!
## Code
```java
class Solution {
    public int missingElement(int[] nums, int k) {
        int totalMissing = (nums[nums.length - 1] - nums[0]) - (nums.length - 1);
        if(k > totalMissing) return nums[nums.length - 1] + k - totalMissing;
        int start = 0;
        int end = nums.length - 1;
        while(start < end){
            int mid = start + (end - start) / 2;
            int missingUntilMid = nums[mid] - nums[0] - mid;
            if(missingUntilMid >= k){
                end = mid;
            }else {
                start = mid + 1;
            }
        }
        return nums[0] + k + start - 1;
    }
}
```