# 977. Squares of a Sorted Array
* 一刷：7:53 （✅）
## Keypoint
* `new` another array (`int [] res = new int [nums.length]`) to store the compared result.

***
# 209. Minimum Size Subarray Sum
* **一刷: 35:05 (❌)**

## My Code
```
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int min = Integer.MAX_VALUE;
        int left = 0;
        int right = 0;
        int sum = 0;
        for(;right <= nums.length - 1; right ++ ){
            sum = sum + nums[right];
            if (sum >= target){
                min = min < right - left + 1 ? min : right - left + 1;
                for (;left < right; ){
                    sum = sum - nums[left];
                    left ++;
                    System.out.println("left :" + left);
                    System.out.println("right :" + right);
                    if(sum < target){
                        continue; //❌应该是break！不然right压根不动了
                    }else{
                        min = min < right - left + 1 ? min : right - left + 1;
                    }
                }
            }
        }
        return min == Integer.MAX_VALUE ? 0 : min;
    }
}
```
### Problem
* `continue`和`break`跳出loop的范围不清楚！Don't worry, break顶多也就关心当前的loop，不可能跳出整个nested loop!!
  * `continue` : Skip the execution of any remaining code in the loop body for the **current iteration**, and control the jumps to the beginning of the loop for the next iteration. ==> If there is a `nested loop`, and `continue` in the inner one, it will **not** stop the whole inner iteration!!!
  * `break`:  The loop is terminated immediately, and control jumps to the **next statement** following the loop. ==>If there is a `nested loop`, and `break` in the inner one, it will **stop** the whole inner iteration!!! (It's often used to exit a loop prematurely when a certain condition is met, regardless of the loop's original termination condition.)
* `Slide Window` 
  * 似滑非滑，反而将代码变复杂。直接使用`while`来控制left的移动
* Integer.MAX_VALUE
## Improved Code
```
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int right = 0;
        int left = 0;
        int min = Integer.MAX_VALUE;
        int sum = 0;
        for (; right < nums.length; right ++){
            sum = sum + nums[right];
            //🌟改进地方，1.通过while来简化代码；2.Math.min来选小的
            while(target <= sum){
                sum = sum - nums[left];
                min = Math.min(min,right-left+1);
                left ++;
            }
            //
        }
        return min == Integer.MAX_VALUE ? 0:min;
    }
}
```
***
# 59. Spiral Matrix II
* 一刷: 32:55 (✅)
## Keypoint:
* `i` is `row`, `j` is `col`