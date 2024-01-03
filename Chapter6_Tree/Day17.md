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
***
# 257. Balanced Tree Paths
* **一刷:31:33(❌)**
* [257. Balanced Tree Paths](https://leetcode.com/problems/binary-tree-paths/)
## Questions
### Q1: 如何在分流的时候复制之前的内容？
* 通过一个`List<Integer> path ` 来存储路径，并且在每次到底之后，进行遍历输出结果再返回
## My Idea
![image](https://github.com/TomasZhu0321/LeetCode_Algorithm/blob/main/Chapter6_Tree/img/257_1.jpeg)
* 通过Queue来遍历，如果左边右边都没有就加入`List res`,如果有一边存在，就`append`。尝试通过`while`来自动复制
* 问题是，这样也没有自动复制，因为哪怕在if中复制了一个新的，但如何确定底部节点对应的上层是谁？
### 错误代码
```java
class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res = new LinkedList<>();
        Queue<TreeNode> que = new LinkedList<>();
        que.offer(root);
        StringBuilder sb = new StringBuilder(String.valueOf(root.val));
        while(!que.isEmpty()){
            TreeNode poll = que.poll();
            if(poll.left != null) {
                sb.append(String.valueOf(poll.val));
                que.offer(poll.left);
            }
            if(poll.right != null) {
                sb.append(String.valueOf(poll.val));
                que.offer(poll.right);
            }
            res.add(sb.toString());
            sb = new StringBuilder("");
        }
        return res;
    }
}
```
## 正确Idea
### **回溯法**
* 本地的需求其实是记录每次recursion的路径，也就是每次到底的时候，return
* 回溯法是通过一个`List<Integer> path`来将遍历的内容存入进path中
* 在每次`到底`时，进行遍历然后添加进结果
* ❗️需要注意(难理解点)的是
  * `回溯`的动作通过,`path.remove(last)`; 来实现
  * `回溯`和`递归`应该包含在`同一个if语句`之下。理解：当一个递归结束，也就是到底时，会在开始if判断node结点中存入了结果，那么应该在上一层remove（也就是回溯）
### 正确Code
```java
class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res = new LinkedList<>();
        if(root==null) return res;
        List<Integer> path = new LinkedList<>();
        traversal(root,res,path);
        return res;
    }
    public void traversal(TreeNode root, List<String> res, List<Integer>path){
        path.add(root.val);
        if(root.left == null && root.right == null){
            StringBuilder sb = new StringBuilder();
            for(int i = 0; i < path.size() - 1; i ++){
                sb.append(String.valueOf(path.get(i)));
                sb.append("->");
            }
            sb.append(String.valueOf(path.get(path.size() - 1)));
            res.add(sb.toString());
        }
        if(root.left!=null){
            traversal(root.left,res,path);
            path.remove(path.size() - 1);
        }
        if(root.right != null){
            traversal(root.right, res, path);
            path.remove(path.size() - 1);
        }
    }
}
```
***
# 404. Sum of Left Leaves
* **一刷:32:03(❌)**
* [404. Sum of Left Leaves](https://leetcode.com/problems/sum-of-left-leaves/description/)

## Keypoints
* 终止条件依然可以是`if(root==null) return 0;`,因为`postTraversal`逻辑,我的sum计算可以放在 `中` 这一步
* 一定要分析清楚题目要求的条件是什么，也就是`逻辑`这一步，不要盲目一上来就写，通常逻辑处理放在`中`这一步

## Code
```java
class Solution {
    public int sumOfLeftLeaves(TreeNode root) {
        if(root == null) return 0;
        int left = sumOfLeftLeaves(root.left);
        int right = sumOfLeftLeaves(root.right);
        int sum = left + right;
        if(root.left != null && root.left.left == null && root.left.right == null){
            sum = sum + root.left.val;
        }
        return sum;       
    }
}
```
