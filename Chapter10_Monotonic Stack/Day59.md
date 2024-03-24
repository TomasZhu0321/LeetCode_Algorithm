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