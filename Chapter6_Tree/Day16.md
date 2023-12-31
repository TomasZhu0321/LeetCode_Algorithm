# 104. Maximum Depth of Binary Tree
* **一刷:32:04 (❌)**
* [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
## Questions
### 1.Depth的记录应该是在“去”还是“回”
* “回”。本题采用postOrder, which is `left | right | val`的逻辑，树的height就是maximum的depth。在traversal逻辑中，不通过left和right的遍历来增加高度, `postOrderMax(root.left,res ++)`(❌),而是在`val`中添加对height记录的逻辑
***
## Keypoints
* 对于使用Recursion迭代record 数字的增加,不要害怕返回`int`! 就想像成这个数字自动被记录了,也不用专门设置一个res来记录, unnecessary! 
***
## My wrong code before
![image](https://github.com/TomasZhu0321/LeetCode_Algorithm/blob/main/Chapter6_Tree/img/104_Q1.png)
## Code Answer
```java
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
***
# 559. Maximum Depth of N-ary Tree
* **一刷:13:55(✅)**
* [559.Maximum Depth of N-ary Tree](https://leetcode.com/problems/maximum-depth-of-n-ary-tree/description/)

## Keypoints
* 不应该在for循环中添加增加height逻辑，而是在return中选择出最“高“的，然后++

## My wrong code before
![image](https://github.com/TomasZhu0321/LeetCode_Algorithm/blob/main/Chapter6_Tree/img/559_1.png)

## Code
```java
class Solution {
    public int maxDepth(Node root) {
        if(root == null){
            return 0;
        }
        int max = 0;
        for(Node n : root.children){
            int depth = maxDepth(n);
            max = Math.max(depth,max);
        }
        return max + 1;
    }
}
```
***
# 111. Minimum Depth of Binary Tree
* 一刷:23:04(✅)
* [111.Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/description/)
  
## Keypoints
* `leaf node`指的是left和right都是`null`的情况
* 在return的条件判断中，依然可以保持`if(root == null)`,因为在主体logic中,需要添加`if(left == 0) return right + 1;`. 也就是如果左边没有，右边有的情况，应该直接按照right的height + 1
* `Complete Full Tree`的nodes个数是`2^n - 1`. 本题如果通过性质来做:
  * 通过`int leftDep`和`int rightDep`来记录左右深度
  * `if(leftDep == rightDep) return (2 << leftDepth) - 1;` 如果`不相等`，就继续遍历，直到是`complete full tree` `return countNodes(root.left) + countNodes(root.right) + 1;`
  * `leftDepth` 和 `rightDepth`是通过不断往下探索得出
## Code
```java
class Solution {
    public int minDepth(TreeNode root) {
        if(root == null){
            return 0;
        }
        int left = 0;
        int right = 0;
        left = minDepth(root.left);
        right = minDepth(root.right);
        if(left == 0) return right + 1;
        if(right == 0) return left + 1;
        return Math.min(left,right) + 1;
    }       
}
```
***
# 222. Count Complete Tree Nodes
* 一刷:3:02(✅)
* [222. Count Complete Tree Nodes](https://leetcode.com/problems/count-complete-tree-nodes/description/)

## My Code
* Recursion
```java
class Solution {
    public int countNodes(TreeNode root) {
         if(root == null){
             return 0;
         }
         int left = countNodes(root.left);
         int right = countNodes(root.right);
         return left + right + 1;
    }
}
```
* 利用`complete full tree`性质
```java
class Solution {
    /**
     * 针对完全二叉树的解法
     *
     * 满二叉树的结点数为：2^depth - 1
     */
    public int countNodes(TreeNode root) {
        if (root == null) return 0;
        TreeNode left = root.left;
        TreeNode right = root.right;
        int leftDepth = 0, rightDepth = 0; // 这里初始为0是有目的的，为了下面求指数方便
        while (left != null) {  // 求左子树深度
            left = left.left;
            leftDepth++;
        }
        while (right != null) { // 求右子树深度
            right = right.right;
            rightDepth++;
        }
        if (leftDepth == rightDepth) {
            return (2 << leftDepth) - 1; // 注意(2<<1) 相当于2^2，所以leftDepth初始为0
        }
        return countNodes(root.left) + countNodes(root.right) + 1;
    }
}
```
