# 1005. Maximize Sum Of Array After K Negations
* **一刷:26：09(✅)**
* [1005. Maximize Sum Of Array After K Negations](https://leetcode.com/problems/maximize-sum-of-array-after-k-negations/description/)

## My Code
* 思路：
  * 排序，然后分情况讨论
    * <0, 如果还没到底,计算minus;不然就是每次改变符号变正
    * >0, 需要留意是不是绝对值最小值, 且minus推一步的时候，k-i就好
```java
class Solution {
    public int largestSumAfterKNegations(int[] nums, int k) {
        Arrays.sort(nums);
        for(int i = 0; i < k; i ++){
            if(nums[i] == 0 ){
               break;
            }
            if(nums[i] < 0){
                if(i  >= nums.length - 1){
                    int minus_2 = ((k - i)%2) == 1?-1:1;
                    nums[i] = nums[i] * minus_2;
                    break;
                }
                nums[i] = -nums[i];
                continue;
            }
            if(nums[i] > 0){
                if(i > 0){
                    if(Math.abs(nums[i]) > Math.abs(nums[i - 1])){
                        int minus_1 = ((k - i)%2) == 1?-1:1;
                        nums[i - 1] = nums[i - 1] * minus_1;
                        break;
                    }
                }
                int minus = ((k - i)%2) == 1?-1:1;
                nums[i] = nums[i] * minus;
                break;
            }
        }
        int res = 0 ;
        for(int i : nums){
            res = res + i;
        }
        return res;
    }
}
```