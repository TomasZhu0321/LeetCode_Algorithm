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