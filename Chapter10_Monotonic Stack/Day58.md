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