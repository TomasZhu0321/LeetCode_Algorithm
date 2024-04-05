# 724. Find Pivot Index
* **一刷:14:22(✅)**
* [724. Find Pivot Index](https://leetcode.com/problems/find-pivot-index/)

## Code
``` java
class Solution {
    public int pivotIndex(int[] nums) {
        if (nums.length == 1) return 0;
        int [] right = new int [nums.length];
        int [] left = new int [nums.length];
        for(int i = nums.length - 2; i >= 0 ; i --){
            right[i] = right[i + 1] + nums[i + 1];
        }
        for(int i = 1; i <= nums.length - 1; i ++){
            left[i] = left[i - 1] + nums[i - 1];
        }
        for(int i = 0 ; i < nums.length; i ++){
            if(left[i] == right[i]) return i;
        }
        return -1;
    }
}
```
* 还有一种方法是for求出总和，然后再来一个for，分别计算leftSum和rightSum看是否相等
```java
class Solution {
    public int pivotIndex(int[] nums) {
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i]; // 总和
        }
        int leftSum = 0;
        int rightSum = 0;
        for (int i = 0; i < nums.length; i++) {
            leftSum += nums[i];
            rightSum = sum - leftSum + nums[i]; // leftSum 里面已经有 nums[i]，多减了一次，所以加上
            if (leftSum == rightSum) {
                return i;
            }
        }
        return -1; // 不存在
    }
}
```
***