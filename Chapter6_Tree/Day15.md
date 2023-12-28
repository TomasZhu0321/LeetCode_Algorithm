# Level Order Traversal
* 借助 `queue`来实现
  * `Queue<TreeNode> que = new LinkedList<>();`
  * `que.offer()`入queue, `que.poll()`出queue, `que.size()`queue的长度, `queue.isEmpty()`queue是否为空
  * 层序遍历的时候，通过**fixed size**来distinguish each level!! 
# 102. Binary Tree Level Order Traversal
* **一刷: 30:05 (❌)**
* [102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/submissions/)
  
## My questions
* Q1: 如何区分单层是否clear？
  * 通过**固定size**且**内部while**

## Code
```
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new LinkedList<List<Integer>>();
        levelTraversal(root,res);
        return res;
    }
    public void levelTraversal(TreeNode root, List<List<Integer>> res){
        if(root == null){
        return ;
        }
        Queue<TreeNode> que = new LinkedList<>();
        que.offer(root);
        while(!que.isEmpty()){
            List<Integer> inList = new LinkedList<>();
            int len = que.size();
            while(len > 0){
                TreeNode tmp = que.poll();
                inList.add(tmp.val);
                len --;
                if(tmp.left != null){que.offer(tmp.left);}
                if(tmp.right != null){que.offer(tmp.right);}
            }
            res.add(inList);
        }
    }
}
```
***
# 107. Binary Tree Level Order Traversal II
* 一刷：8:04 （✅）
* [107. Binary Tree Level Order Traversal II](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/description/)

***
# 199. Binary Tree Right Side View
* 一刷：7:00 （✅）
* [199. Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/description/)

***
# 637. Average of Levels in Binary Tree
* 一刷：8:00 （✅
* [637. Average of Levels in Binary Tree](https://leetcode.com/problems/average-of-levels-in-binary-tree/description/)

***
# 429. N-ary Tree Level Order Traversal
* 一刷：23:00 （✅
* [429. N-ary Tree Level Order Traversal](https://leetcode.com/problems/n-ary-tree-level-order-traversal/description/)

## Keypoints
* 使用 `for(Node n: treeNodes.children)` 循环遍历来访问List上元素
***
# 515. Find Largest Value in Each Tree Row
* 一刷：6:44 (✅)
* [515. Find Largest Value in Each Tree Row](https://leetcode.com/problems/find-largest-value-in-each-tree-row/description/)

# 116. Populating Next Right Pointers in Each Node
* 一刷：30:44 (✅)
* [116. Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/description/)

***
# 226. Invert Binary Tree
* 一刷：26:04 （✅）[有点卡壳]
* [226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/description/)
  
## Keypoints
* 递归法：
  * 真正的逻辑是在一开始的`swap`，而不是之后的遍历（中左右和中右左其实都可以）
* 迭代法：
  * 在push入stack时，需要检查是否为null
  

## Code
### 递归法
```
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if(root == null){return root;}
        reverseTree(root);
        return root;
    }
    public void reverseTree(TreeNode root){
        if(root == null){return ;}
        TreeNode tmp = root.right;
        root.right = root.left;
        root.left = tmp;
        reverseTree(root.left);
        reverseTree(root.right);
    }
}
```
### 迭代法
```
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if(root == null )return root;
        reverseTree(root);
        return root;
    }
    public void reverseTree(TreeNode root){
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while(!stack.isEmpty()){
            TreeNode tmp = stack.pop();
            TreeNode temp = tmp.right;
            tmp.right = tmp.left;
            tmp.left = temp;
            if(tmp.right != null){
                stack.push(tmp.right);
            }
            if(tmp.left != null){
                stack.push(tmp.left);
            }
        }
    }
}
```
***
# 101. Symmetric Tree
* 一刷：23:44 （✅）
* [101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/description/)

## My code
```
class Solution {
    public boolean isSymmetric(TreeNode root) {
        int result = 0;
        int res = isSym(root.left,root.right,result);
        return res == 0 ? true:false;
    }
    public int isSym(TreeNode root_left, TreeNode root_right,int result){
        if((root_left == null && root_right != null) || (root_right == null && root_left != null)){
            return -1;
        }
        else if((root_left == null)){
            return 0;
        }
        else if((root_right == null)){
            return 0;
        }
        else if((root_left.val != root_right.val)){
            return -1;
        }
        result = result + isSym(root_left.left, root_right.right,result);
        result = result + isSym(root_left.right,root_right.left,result);
        return result;
    }
}
```
