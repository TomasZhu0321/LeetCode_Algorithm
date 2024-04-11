# 129. Sum Root to Leaf Numbers
* **一刷:22:46(✅)**
* [129. Sum Root to Leaf Numbers](https://leetcode.com/problems/sum-root-to-leaf-numbers/)

## My Code
* 思路:通过backtracking回退
```java
class Solution {
    List<List<Integer>> res = new LinkedList<>();

    public int sumNumbers(TreeNode root) {
        List<Integer> tmp = new LinkedList<>();
        backTracking(root, tmp);
        int ans = 0;
        for (int i = 0; i < res.size(); i++) {
            List<Integer> inList = res.get(i);
            StringBuilder sb = new StringBuilder();
            for (int j = 0; j < inList.size(); j++) {
                sb.append(String.valueOf(inList.get(j)));
            }
            ans += Integer.parseInt(sb.toString());
        }
        return ans;
    }

    private void backTracking(TreeNode node, List<Integer> tmp) {
        tmp.add(node.val);
        if (node.left == null && node.right == null) {
            res.add(new LinkedList<>(tmp));
            return;
        }
        if (node.left != null) {
            backTracking(node.left, tmp);
            tmp.removeLast();
        }
        if (node.right != null) {
            backTracking(node.right, tmp);
            tmp.removeLast();
        }
        return;
    }
}
```