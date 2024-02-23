# 530. Minimum Absolute Difference in BST
* **一刷:19:46(❌)**
* [530. Minimum Absolute Difference in BST](https://leetcode.com/problems/minimum-absolute-difference-in-bst/)

## Tree问题：递归遍历记录pre和cur两个指针
* 技巧:在class之中定义`全局变量`。
  * 通过全局变量，不用put指针到递归函数中
  * 可以直接返回`res`值

## Code
```java
class Solution {
    TreeNode pre;
    int res = Integer.MAX_VALUE;
    public int getMinimumDifference(TreeNode root) {
        if(root == null)return 0;
        traversal(root);
        return res;
    }
    private void traversal(TreeNode root){
        if(root == null) return ;
        traversal(root.left);
        if(pre!=null){
            res = Math.min(res, root.val - pre.val);
        }
        pre = root;
        traversal(root.right);
    }
}
```
