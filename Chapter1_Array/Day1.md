# 704. Binary Search
* 一刷：23:04（✅）
## Keypoint
* Bitwise operators such as "<<" ">>" have higher precedence than arithmetic operators like "+" "-" 

    => which means `((right-left)>>1))+left` instead of `(right-left)>>1+left`

![image](https://github.com/TomasZhu0321/LeetCode_Algorithm/blob/main/Chapter1_Array/img/704_1.png)

***
# 27. Remove Element
* 一刷：7:57 （✅）
## Keypoint
* `fast` and `slow` point, if `nums[fast] == val` move fast; Otherwise, move together.