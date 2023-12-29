# 104. Maximum Depth of Binary Tree
* **一刷:32:04 (❌)**

## Questions
### 1.Depth的记录应该是在“去”还是“回”
* “回”。本题采用postOrder, which is `left | right | val`的逻辑，树的height就是maximum的depth。在traversal逻辑中，不通过left和right的遍历来增加高度, `postOrderMax(root.left,res ++)`(❌),而是在`val`中添加对height记录的逻辑
***
## Keypoints
* 对于使用Recursion迭代record 数字的增加,不要害怕返回`int`! 就想像成这个数字自动被记录了,也不用专门设置一个res来记录, unnecessary! 
***
## My faults code
![image](https://github.com/TomasZhu0321/LeetCode_Algorithm/blob/main/Chapter6_Tree/img/104_Q1.png)
## Code Answer
```
class solution {
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int leftDepth = maxDepth(root.left);
        int rightDepth = maxDepth(root.right);
        return Math.max(leftDepth, rightDepth) + 1;
    }
}
```