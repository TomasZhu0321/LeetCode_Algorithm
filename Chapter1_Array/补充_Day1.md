# 1365. How Many Numbers Are Smaller Then the Current Number
* **一刷:12：44(✅)**
* [1365. How Many Numbers Are Smaller Then the Current Number](https://leetcode.com/problems/how-many-numbers-are-smaller-than-the-current-number/)

## 知识点
* **数组的拷贝**: `System.arraycopy(nums,0,tmp,0,nums.length);` //(src数组)|(拷贝起始位置)|(目标数组)|(目的地起始位置)|(长度)

## My Code
```java
class Solution {
    public int[] smallerNumbersThanCurrent(int[] nums) {
        int [] tmp = new int [nums.length];
        System.arraycopy(nums,0,tmp,0,nums.length);
        Arrays.sort(nums);
        Map<Integer,Integer> map = new HashMap<>();
        int endIndex = nums.length - 1;
        while(endIndex >= 0){
            if(endIndex != 0 && nums[endIndex] != nums[endIndex - 1]){
                map.put(nums[endIndex], endIndex);
            }
            if(endIndex == 0){
                map.put(nums[endIndex], 0);
            }
            endIndex --;
        }
        int [] res = new int [nums.length];
        for(int i = 0; i < tmp.length; i ++){
            res[i] = map.get(tmp[i]);
        }
        return res;
    }
}
```
***
# 941. Valid Mountain Array
* **一刷:11：55(✅)**
* [941. Valid Mountain Array](https://leetcode.com/problems/valid-mountain-array/)

## My Code
* For some reason, 将while的逻辑单独拆分开来的速度比合在一起快
```java
class Solution {
    public boolean validMountainArray(int[] arr) {
        if (arr.length < 3) { // 此时，一定不是有效的山脉数组
            return false;
        }
        // 双指针
        int left = 0;
        int right = arr.length - 1;
        // 注意防止指针越界
        while (left + 1 < arr.length && arr[left] < arr[left + 1]) {
            left++;
        }
        // 注意防止指针越界
        while (right > 0 && arr[right] < arr[right - 1]) {
            right--;
        }
        // 如果left或者right都在起始位置，说明不是山峰
        if (left == right && left != 0 && right != arr.length - 1) {
            return true;
        }
        return false;
    }
}
```