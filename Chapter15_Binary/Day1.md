# 34. Find First and Last Position of Element in Sorted Array
* **一刷:11：45(✅)**
* [34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

## My Code
### 注意
* 二分法用while，记得start和end 要 ++和--，否则死循环
  
### Code
```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int [] res = {-1,-1};
        if(nums.length == 0) return res;
        int start = 0;
        int end = nums.length - 1;
        while(start <= end){
            int index = ((end - start)/2) + start; 
            if(nums[index]!=target){
                if(nums[index] < target){
                    start = index;
                    start ++;
                }
                else {
                    end = index;
                    end --;
                }
            }else {
                int left = index;
                int right = index;
                while(left >= 0 && nums[left] == target){
                    res[0] = left;
                    left --;
                }
                while(right <nums.length && nums[right] == target){
                    res[1] = right;
                    right ++;
                }
                break;
            }
        }
        return res;
    }
}
```