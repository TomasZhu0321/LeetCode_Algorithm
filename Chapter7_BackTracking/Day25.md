# 216. Combination Sum III
* **一刷:18:22(✅)**
* [216. Combination Sum III](https://leetcode.com/problems/combination-sum-iii/)
## My Code
```java
class Solution {
    List<List<Integer>> res = new LinkedList<>();
    List<Integer> tmp = new LinkedList<>();
    public List<List<Integer>> combinationSum3(int k, int n) {
        backTracking(k, n , 1);
        return res;
    }
    private void backTracking(int k, int n, int startIndex){
        if(tmp.size() == k && n == 0){
            res.add(new LinkedList<>(tmp));
            return;
        }
        for(int i = startIndex; i <= n - (k - tmp.size()) + 1; i ++ ){
            if (i <= 9){
            tmp.add(i);
            backTracking(k, n - i, i + 1);
            tmp.removeLast();
            }
        }
    }
}
```
***

# 17. Letter Combinations of a Phone Number
* **一刷:50:22(❌)**
* [17. Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)
## 字符串操作
* StingBuilder 灵活 “添加(append)/删除(deleteCharAt)
* toString()转换成String
## Code
* 从8开始有偏移量
```java
class Solution {
    List<String> res = new LinkedList<>();
    String tmp = "";
    public List<String> letterCombinations(String digits) {
        if (digits == null || digits.length() == 0) {
            return res;
        }
        backTracking(digits,0);
        return res;
    }
    private void backTracking(String digits,int cur){
        if(tmp.length() == digits.length()){
            res.add(new String(tmp));
            return;
        }
        int n ;
        if(digits.charAt(cur) == '7' || digits.charAt(cur) == '9' ){
            n = 4;
        }else {
            n = 3;
        }
        for (int i = 0; i < n; i ++){
            // tmp = tmp + Integer.toString(((digits.charAt(cur) -'0') - 2) + 97 + i);
            tmp = tmp + (char)(((digits.charAt(cur) - '0') - 2) * 3 + 97 + i + (digits.charAt(cur) >= '8' ? 1 : 0));
            backTracking(digits,cur + 1);
            tmp = tmp.substring(0,tmp.length() - 1);
        }

    }
}
```