# Recursion(递归)
自己调用自己的过程
* 三部曲
  * **确定递归函数`参数`和`返回值`** : 确定哪些参数是递归的过程中需要处理的，那么就在递归函数里加上这个参数， 并且还要明确每次递归的返回值是什么进而确定递归函数的返回类型
  * **确定`终止条件`**: 写完了递归算法, 运行的时候，经常会遇到栈溢出的错误，就是没写终止条件或者终止条件写的不对，操作系统也是用一个栈的结构来保存每一层递归的信息，如果递归没有终止，操作系统的内存栈必然就会溢出
  * **确定`单层递归`的逻辑**: 确定每一层递归需要处理的信息。在这里也就会**重复调用自己**来实现递归的过程

## 144. Binary Tree Preorder Traversal
* 题目:[144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)
### My Code
```
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new LinkedList<>();
        preorder(root, res);
        return res;
    }
    public void preorder (TreeNode root, List<Integer> res){
        if(root == null){
            return;
        }
        res.add(root.val);
        preorder(root.left, res);
        preorder(root.right, res);
    }
}
```
## 145. Binary Tree Postorder Traversal
* 题目:[145. Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/)

## 94. Binary Tree Inroder Traversal
* 题目:[94. Binary Tree Inroder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

***
# Iteration(迭代法)
* 通过Stack来实现迭代
* Preorder和Inorder方法不一样，因为Inorder的**访问元素**和**处理元素**的顺序不一样
## 144. Binary Tree Preorder Traversal
* 题目:[144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)
### Keypoints
* 通过将node `push`进 Stack中，然后通过`pop`来访问`leaves`实现遍历
* 空节点不入stack
### My Code
``` class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new LinkedList<>();
        if (root == null){
            return res;
        }
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while(!stack.isEmpty()){
            TreeNode tmp = stack.pop();
            if(tmp != null){
            res.add(tmp.val);
            stack.push(tmp.right);
            stack.push(tmp.left);
            }
        }
        return res;
    }
}
```
## 145. Binary Tree Postorder Traversal
* 题目:[145. Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/)
### Keypoint
* 通过`Collections.reverse(xx)`在pre的基础上改进就可以

## 94. Binary Tree Inroder Traversal
* 题目:[94. Binary Tree Inroder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)
### Keypoints
* 因为访问元素和处理元素的顺序不一样，inorder需要先到达底部然后再存入res。因此通过`TreeNode cur`指针来实现遍历（访问），通过`Stack stack`来实现处理
### My Code
```
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if(root == null){
            return res;
        }
        Stack<TreeNode> sta = new Stack<>();
        TreeNode cur = root;
        while(cur != null || !sta.isEmpty()){
            if(cur!=null){
                sta.push(cur);
                cur = cur.left;
            }else{
                TreeNode tmp = sta.pop();
                res.add(tmp.val);
                cur = tmp.right;
            }
        }
        return res;
    }
}
```