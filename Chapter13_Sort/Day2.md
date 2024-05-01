# 75. Sort Colors
* **一刷:36:50(✅)**
* [75. Sort Colors](https://leetcode.com/problems/sort-colors/)

## 思路
* 通过找到固定值，l: 存放最小的0; r: 存放最大的2
* 通过i来进行遍历，当i是0，更新left； 当i是2，更新2。最后的结果自然而然就是排序好的！
```java
class Solution {
  public void sortColors(int[] nums) {
    int l = 0;
    int r = nums.length - 1;

    for (int i = 0; i <= r;)
      if (nums[i] == 0)
        swap(nums, i++, l++);
      else if (nums[i] == 1)
        i++;
      else
        swap(nums, i, r--);
  }

  private void swap(int[] nums, int i, int j) {
    final int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
  }
}
```