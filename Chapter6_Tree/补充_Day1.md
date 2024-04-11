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
# 1382. Balance a Binary Search Tree
* **一刷:40:46(❌)** [重刷]
* [1382. Balance a Binary Search Tree](https://leetcode.com/problems/balance-a-binary-search-tree/)

## 思路
* 通过**inorder-traversal**按照ascending遍历Tree
* 然后通过二分法，递归构造BST
* ❗️退出条件:`left > right`;
```java
class Solution {
    ArrayList <Integer> res = new ArrayList<Integer>();
    private void travesal(TreeNode cur) {
            if (cur == null) return;
            travesal(cur.left);
            res.add(cur.val);
            travesal(cur.right);
        }
    private TreeNode getTree(ArrayList <Integer> nums, int left, int right) {
        if (left > right) return null;
        int mid = left + (right - left) / 2;
        TreeNode root = new TreeNode(nums.get(mid));
        root.left = getTree(nums, left, mid - 1);
        root.right = getTree(nums, mid + 1, right);
        return root;
    }
    public TreeNode balanceBST(TreeNode root) {
        travesal(root);
        return getTree(res, 0, res.size() - 1);
    }
}
```