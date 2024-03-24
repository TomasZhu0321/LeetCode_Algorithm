# 739. Daily Temperature
* **一刷:30：04(✅)**
* [739. Daily Temperature](https://leetcode.com/problems/daily-temperatures/)

## 知识点
* Stack已经被淘汰，使用Deque
`Deque <> stack = new LinkedList<>();`
* 存放下标就可以，直接在原数组上访问

## My Code
```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        Deque<Integer> stack = new LinkedList<>();
        int [] res = new int [temperatures.length];
        stack.push(0);
        for(int i = 1; i < temperatures.length; i ++){
            while(!stack.isEmpty() && temperatures[i] > temperatures[stack.peek()]){
                int idx = stack.pop();
                res[idx] = i - idx;
            }
            stack.push(i);
        }
        return res;
    }
}
```
***
# 496. Next Greater Element I
* **一刷:20：04(✅)**
* [496. Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/)

## My Code
```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        Deque<Integer> stack = new LinkedList<>();
        int [] nums2Res = new int [nums2.length];
        Arrays.fill(nums2Res,-1);
        stack.push(0);
        for(int i = 1; i < nums2Res.length; i ++){
            while(!stack.isEmpty() && nums2[i] > nums2[stack.peek()] ){
                nums2Res[stack.peek()] = nums2[i];
                stack.pop();
            }
            stack.push(i);
        }
        int [] res = new int [nums1.length];
        for(int i = 0; i < nums1.length; i ++){
            for(int j = 0; j < nums2.length; j ++){
                if(nums1[i] == nums2[j]){
                    res[i] = nums2Res[j];
                }
            }
        }
        return res;
    }
}
```