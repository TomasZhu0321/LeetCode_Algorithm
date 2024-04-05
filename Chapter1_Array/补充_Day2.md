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
# 34. Find First and Last Position of Element in Sorted Array
* **一刷:15:22(✅)**
* [34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

## Code
* Log(n)的复杂度，通常就是**二分法**
```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int index = findBinary(nums, target);
        int[] res = { -1, -1 };
        if (index == -1)
            return res;
        int left = index;
        int right = index;
        while (left >= 0 && nums[left] == target) {
            left--;
        }
        while (right <= nums.length - 1 && nums[right] == target) {
            right++;
        }
        res[0] = left + 1;
        res[1] = right - 1;
        return res;

    }

    public int findBinary(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        while (left <= right) {
            int mid = ((right - left) / 2) + left;
            if (nums[mid] == target) {
                return mid;
            }
            if (nums[mid] < target) {
                left = mid + 1;
            }
            if (nums[mid] > target) {
                right = mid - 1;
            }
        }
        return -1;
    }
}
```
***
# 922. Sort Array By Parity II
* **一刷:15:22(✅)**
* [922. Sort Array By Parity II](https://leetcode.com/problems/sort-array-by-parity-ii/)

## My Code
* 思路：通过cur和next，每次满足就交换，然后更新next = cur；
* 问题：时间复杂度是O(n^2)
```java
class Solution {
    public int[] sortArrayByParityII(int[] nums) {
        int cur = 0;
        int next = 0;
        for (; next < nums.length; next++) {
            if (cur % 2 == nums[next] % 2) {
                int tmp = nums[cur];
                nums[cur] = nums[next];
                nums[next] = tmp;
                cur++;
                next = cur;
            }
        }
        return nums;
    }
}
```

* 优化：通过定义odd和even指针，不满足条件的时候odd和even指针交换就可以了。需要开辟一个`int [] result`来存放结果数组 
* 时间复杂度: 一个for循环搞定，时间复杂度O(n)
```java
class Solution {
    public int[] sortArrayByParityII(int[] nums) {
        int even = 0;
        int odd = 1;
        int[] result = new int[nums.length];
        for(int i = 0; i < nums.length; i ++){
            if(nums[i]%2 == 0){
                result[even] = nums[i];
                even = even + 2;
            }
            if(nums[i] % 2 == 1){
                result[odd] = nums[i];
                odd = odd + 2;
            }
        }
        return nums;
    }
}
```
***

# 35. Search Insert Position
* **一刷:10:22(✅)**
* [35. Search Insert Position](https://leetcode.com/problems/search-insert-position/)

## My Code
```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        while (left <= right) {
            int mid = ((right - left) / 2) + left;
            if (nums[mid] == target) {
                return mid;
            }
            if (nums[mid] > target) {
                right = mid - 1;
            }
            if (nums[mid] < target) {
                left = mid + 1;
            }
        }
        return left;
    }
}
```