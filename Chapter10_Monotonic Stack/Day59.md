# 503. Next Greater Element II
* **一刷:45：04(✅)**
* [503. Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/)

## My Code
```java
class Solution {
    public int[] nextGreaterElements(int[] nums) {
        Deque<Integer> stack = new LinkedList<>();
        int[] res = new int[nums.length];
        Arrays.fill(res, -1);
        if (nums.length == 1) {
            return res;
        }
        stack.push(0);
        int cur = 1;
        int circle = 0;
        while (cur < stack.peek() || circle == 0) {
            while (!stack.isEmpty() && nums[cur] > nums[stack.peek()]) {
                int idx = stack.pop();
                res[idx] = nums[cur];
            }
            if(circle > 0 && stack.isEmpty()){
                break;
            }
            if(circle == 0){
                stack.push(cur);
            }
            cur++;
            if (cur > nums.length - 1) {
                cur = 0;
                circle ++;
            }
        }
        return res;
    }
}
```

# 42. Trapping Rain Water
* **一刷:60：04(❌)**
* [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)

## 分析
* stackTop在最开始就赋值
* 在正式的逻辑处理if中，找到当前柱子的高度用于比较
* 注意在left的高度逻辑中，并没有pop出来(因为在之后的`stackTop + int mid = stack.pop()` 会处理！！)
```java
class Solution {
    public int trap(int[] height){
        int size = height.length;

        if (size <= 2) return 0;

        // in the stack, we push the index of array
        // using height[] to access the real height
        Deque<Integer> stack = new LinkedList<Integer>();
        stack.push(0);

        int sum = 0;
        for (int index = 1; index < size; index++){
            int stackTop = stack.peek();
            if (height[index] < height[stackTop]){
                stack.push(index);
            }else if (height[index] == height[stackTop]){
                stack.pop();
                stack.push(index);
            }else{
                int heightAtIdx = height[index];
                while (!stack.isEmpty() && (heightAtIdx > height[stackTop])){
                    int mid = stack.pop();
                    if (!stack.isEmpty()){
                        int left = stack.peek();
                        int h = Math.min(height[left], height[index]) - height[mid];
                        int w = index - left - 1;
                        int hold = h * w;
                        sum += hold;
                        stackTop = stack.peek();
                    }
                }
                stack.push(index);
            }
        }

        return sum;
    }
}
```