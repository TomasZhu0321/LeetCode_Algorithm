# 110. Balanced Binary Tree
* **一刷:21:32(✅)**
* [110. Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/description/)
## Questions
### Q1:如何既record depth 又 判断height difference > 1?
* My solution(能通过)
  * 通过两个递归，一个递归记录depth，一个递归记录高度difference是否>1
* 代码随想录思路
  * 在我的方法上进行了精简。首先还是需要构造一个`getHeight`的递归method。返回的是`int height`
  * 通过`reutrn -1`来讲所有不满足的情况统统归为一类(include: 左边不满足==-1, 右边不满足==-1,新的difference不满足==-1)
  * 在`isBalanced`函数返回`结果`的时候，通过`return res == -1 ? false : true; `来实现最后的boolean判断
## Code
### My Code
```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        if(root == null) return true;
        int left = depth(root.left);
        int right = depth(root.right);
        if(Math.abs(left - right) > 1) return false;
        boolean l = isBalanced(root.left);
        boolean r = isBalanced(root.right);
        return l && r;
    }
    public int depth(TreeNode root){
        if(root == null){
            return 0;
        }
        int left = depth(root.left);
        int right = depth(root.right);
        return Math.max(left,right) + 1;
    }
}
```
### 代码随想录Code
```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        int res = getHeight(root);
        return res == -1 ? false : true;
    }
    public int getHeight(TreeNode root){
        if(root == null ) return 0;
        int leftHeight = getHeight(root.left);
        int rightHeight = getHeight(root.right);
        if(leftHeight == -1) return -1;
        if(rightHeight == -1) return -1;
        if(Math.abs(rightHeight - leftHeight) > 1) return -1;
        return Math.max(leftHeight, rightHeight) + 1;
    }
}
```