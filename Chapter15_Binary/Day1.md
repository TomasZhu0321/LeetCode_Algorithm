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
***
# 33. Search in Rotated Sorted Array
* **一刷:50：45(❌)**
* [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)

## My Code
### 分析
* 二分法找准核心是如果target不在左边区域，那么直接去右边`(start = mid  + 1);`; 不在右边区域，那么直接去左边`(end = mid - 1);`;
* 题目重点就是找准如何判断是否在左边内或者右边内
* 二分法成立的条件就是单调递增(ascending order)的序列！那么为了使二分法成立，就需要先划分清楚哪边是有序的

### Code
```java
class Solution {
    public int search(int[] nums, int target) {
        int start = 0;
        int end = nums.length - 1;
        while(start <= end){
            int mid = start + (end - start)/2;
            if(nums[mid] == target) return mid;
            if(nums[start] <= nums[mid]){
                if(nums[mid] > target && nums[start] <= target){
                    end = mid - 1;
                }else{
                    start = mid + 1;
                }
            }
            else {
                if(nums[mid] < target && target <= nums[end]){
                    start = mid + 1;
                }else{
                    end = mid - 1;
                }
            }
        }
        return -1;
    }
}
```
***
# 162. Find Peak Element
* **一刷:14：45(✅)**
* [162. Find Peak Element](https://leetcode.com/problems/find-peak-element/)

## My Code
```java
class Solution {
    public int findPeakElement(int[] nums) {
        int res = 0;
        int start = 0;
        int end = nums.length - 1;
        if(nums.length == 1) return 0;
        while(start <= end){
            int mid = start + (end - start) / 2;
            //edge cases
            if(mid == 0 && nums[mid + 1] < nums[mid]) return mid;
            if(mid == nums.length - 1 && nums[mid - 1] < nums[mid]) return mid;

            if(mid + 1 < nums.length && nums[mid + 1] > nums[mid]){
                start = mid + 1;
            }
            else if (mid >= 0 && nums[mid] < nums[mid - 1]){
                end = mid - 1;
            }else {
                res = mid ;
                return res;
            }
        }
        return res;
    }
}
```
***
# 278. First Bad Version
* **一刷:11：45(✅)**
* [278. First Bad Version](https://leetcode.com/problems/first-bad-version/)

## My Code
* 找固定的定点的二分法， `right = mid`, 然后判断条件是当`left == right`就跳出循环(因为找到了定点)

```java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int left = 1;
        int right = n;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (isBadVersion(mid)) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return right;
    }
}
```
***
# 74. Search a 2D Matrix
* **一刷:15：45(✅)**
* [74. Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)

## My Code
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int row_start = 0;
        int row_end = matrix.length - 1;
        while(row_start <= row_end){
            int row_mid = row_start + (row_end - row_start) / 2;
            if(row_mid == matrix.length - 1 || (matrix[row_mid][0] <= target && matrix[row_mid + 1][0] > target)){
                int col_start = 0;
                int col_end = matrix[0].length - 1;
                while(col_start <= col_end){
                    int col_mid = col_start + (col_end - col_start)/2;
                    if(matrix[row_mid][col_mid] == target) return true;
                    else if(matrix[row_mid][col_mid] < target) {
                        col_start = col_mid + 1;
                    }else {
                        col_end = col_mid - 1;
                    }
                }
                return false;
            }else {
                if(matrix[row_mid][0] < target){
                    row_start = row_mid + 1;
                }else if(matrix[row_mid][0] > target){
                    row_end = row_mid - 1;
                }
            }
        }
        return false;
    }
}
```

***
# 240. Search a 2D Matrix II
* **一刷:25：45(❌)**
* [240. Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/)

## My Code
* 找到2d matrix的row和col分别ascending的性质，那么从`bottom-left`开始走: 1. 如果 `<target`，说明肯定是在上一行 row --（小的一行，因为这一行之后所有值都大于cur; 2. 如果`>target`, col++
* **倒序** 会让很多有序题变得简单！！
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int row = matrix.length - 1;
        int col = 0;
        while(row >= 0 && col < matrix[0].length){
            if(target == matrix[row][col]) return true;
            else if(matrix[row][col] < target) col ++;
            else{
                row --;
            }
        }
        return false;
    }
}
```
***
# 69. Sqrt(x)
* **一刷:17：45(✅)**
* [69. Sqrt(x)](https://leetcode.com/problems/sqrtx/)

## My Code
* 当结果很大可能超出范围时`(-2,147,483,648 , 2,147,483,647)`，用long
```java
class Solution {
    public int mySqrt(int x) {
        long start = 0;
        long end = x;
        while(start <= end){
            long mid = start + (end - start)/2;
            long res = mid * mid;
            if (x < mid * mid){
                end = mid - 1;
            }
            else if(x > mid * mid){
                start = mid + 1;
            }else {
                return (int)mid;
            }
        }
        return (int) end;
    }
}
```
***
# 540. Single Element in a Sorted Array
* **一刷:25：45(✅)**
* [540. Single Element in a Sorted Array](https://leetcode.com/problems/single-element-in-a-sorted-array/)

## My Code
```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int start = 0;
        int end = nums.length - 1;
        if(end == 0) return nums[0];
        while(start <= end ){
            int mid = start + (end - start)/2;
            if(nums[end]!=nums[end - 1] ) {
                return nums[end];
            }
            if(nums[start] != nums[start + 1]){
                return nums[start];
            }
            if(nums[mid] != nums[mid + 1] && nums[mid] != nums[mid - 1]) return nums[mid];
            if(mid%2 == 0 && nums[mid] != nums[mid + 1]){
                end = mid - 2;
            }
            else if (mid%2 == 1 && nums[mid] != nums[mid + 1]){
                start = mid + 1;
            }
            else if(mid%2 == 1 && nums[mid] == nums[mid + 1]){
                end = mid - 1;
            }
            else if(mid%2 == 0 && nums[mid] == nums[mid + 1]){
                start = mid + 2;
            }
        }
        return -1;
    }
}
```

