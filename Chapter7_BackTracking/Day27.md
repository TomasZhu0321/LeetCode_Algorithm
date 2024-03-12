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
***
# 40. Combination Sum II
* **一刷:30:22(❌)**
* [40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii/description/)

## 问题
### Q1. 如何记录每层的使用？？
* 分析
  * 知道需要记录每层和每枝树的使用情况，但不知道具体如何记录每层？
* 解答
  * 通过一个`boolean used`数组，每次取用之后设置为true
  * 既然无法区分每层，那么就来判断`每枝`！==> `！used[i - 1] && candidates[i] == candidates[i - 1]`表明了当前枝叶重复采用了，那么就是可以的！！ 如果`used[i - 1] == false`说明了不是在**枝叶，而是在层！**
![image](./img/40.png)
## Code
```java
class Solution {
    List<List<Integer>> res = new LinkedList<>();
    List<Integer> tmp = new LinkedList<>();
    boolean[] used;
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        Arrays.sort(candidates);
        used = new boolean[candidates.length];
        Arrays.fill(used, false);
        backTracking(candidates, target, 0);
        return res;
    }

    private void backTracking(int[] candidates, int target, int startIndex) {
        if (target == 0) {
            res.add(new LinkedList<>(tmp));
            return;
        }
        if (target < 0) {
            return;
        }
        for (int i = startIndex; i < candidates.length; i++) {
            if (candidates[i] > target) {
                break;
            }
            if (i > 0 && candidates[i] == candidates[i - 1] && !used[i - 1]) {
                continue;
            }
            tmp.add(candidates[i]);
            used[i] = true;
            target = target - candidates[i];
            backTracking(candidates, target, i + 1);
            tmp.removeLast();
            target = target + candidates[i];
            used[i] = false;
        }
    }
}
```