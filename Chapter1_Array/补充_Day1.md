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
***
# 1207. Unique Number of Occurrences
* **一刷：6：44(✅)**
* [1207. Unique Number of Occurrences](https://leetcode.com/problems/unique-number-of-occurrences/)

## HashTable的三种方法
### 解决问题
* 快速判断一个元素**是否出现集合里**

### 数组实现
* 当规定了**范围**: 可以通过Array来实现HashTable

### Set实现
* 当**不确定**范围

### Map实现
* 需要一对**key-value**来记录

## Code
```java
class Solution {
    public boolean uniqueOccurrences(int[] arr) {
        int[] count = new int[2002];
        for (int i = 0; i < arr.length; i++) {
            count[arr[i] + 1000]++; // 防止负数作为下标
        }
        boolean[] flag = new boolean[1002]; // 标记相同频率是否重复出现
        for (int i = 0; i <= 2000; i++) {
            if (count[i] > 0) {
                if (flag[count[i]] == false) {
                    flag[count[i]] = true;
                } else {
                    return false;
                }
            }
        }
        return true;
    }
}
```
***
# 283. Move Zeroes
* **一刷:5：44(✅)**
* [283. Move Zeroes](https://leetcode.com/problems/move-zeroes/)

## My Code
```java
class Solution {
    public void moveZeroes(int[] nums) {
        if (nums.length == 1) {
            return;
        }
        int cur = 0;
        int next = 1;
        while (next < nums.length) {
            if (nums[cur] == 0 && nums[next] != 0) {
                int tmp = nums[cur];
                nums[cur] = nums[next];
                nums[next] = tmp;
                cur++;
            } else if (nums[cur] == 0 && nums[next] == 0) {
                next++;
            } else {
                cur++;
                next++;
            }
        }
        return;
    }
}
```
* **优化**: 快慢指针，直接快指针将不是0的数放在slow，然后将后面的数赋值为0(因为后面都有一个统一要求，就是0，可以不用每次交换，提高效率)
```java
public void moveZeroes(int[] nums) {
        int slow = 0;
        for (int fast = 0; fast < nums.length; fast++) {
            if (nums[fast] != 0) {
                nums[slow++] = nums[fast];
            }
        }
        // 后面的元素全变成 0
        for (int j = slow; j < nums.length; j++) {
            nums[j] = 0;
        }
    }
```
***
# 189. Rotate Array
* **一刷：38：44(❌)**
* [189. Rotate Array](https://leetcode.com/problems/rotate-array/)

## 整体 ”前移/后移“ 思路
* 通过reverse
  * 大的reverse一次
  * 再分别进行两次小的reverse
```java
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        k %= n ;
        reverse(0,n - 1,nums);
        reverse(0,k - 1, nums);
        reverse(k, n - 1,nums);
        return ;
    }
    public void reverse(int start,int end, int [] nums){
        
        for(int i = start, j = end; i <= j ; i ++, j --){
            int tmp = nums[i];
            nums[i] = nums[j];
            nums[j] = tmp;
        }
    }
}
```