# 39. Combination Sum
* **一刷:20:22(✅)**
* [39. Combination Sum](https://leetcode.com/problems/combination-sum/)

## My Code
```java
class Solution {
    List<List<Integer>> res = new LinkedList<>();
    List<Integer> tmp = new LinkedList<>();
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        backTracking(candidates,target,0);
        return res;
    }
    private void backTracking(int [] candidates, int target, int startIndex){
        if(target == 0){
            res.add(new LinkedList<>(tmp));
            return;
        }
        if (target < 0){
            return;
        }
        for(int i = startIndex ; i < candidates.length; i ++){
            tmp.add(candidates[i]);
            target = target - candidates[i];
            backTracking(candidates,target, i);
            tmp.removeLast();
            target = target + candidates[i];
        }
    }
}
```