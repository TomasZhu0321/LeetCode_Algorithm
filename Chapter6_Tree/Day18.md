# 513. Find Bottom Left Tree Value
* **一刷:10:46(✅)**
* [513. Find Bottom Left Tree Value](https://leetcode.com/problems/find-bottom-left-tree-value/description/?source=submission-ac)
  
## My Code
* 迭代法，记录每一层的最左边，返回最后那个值就可以
```java
class Solution {
    public int findBottomLeftValue(TreeNode root) {
        Queue<TreeNode> que = new LinkedList<>();
        que.offer(root);
        int res = root.val; 
        while(!que.isEmpty()){
            int size = que.size();
            int max = que.size();
            while(size > 0){        
                TreeNode tmp = que.poll();
                if(max == size){res = tmp.val;}
                size --;
                if(tmp.left != null) que.offer(tmp.left);
                if(tmp.right != null) que.offer(tmp.right);
            }
        }
        return res;
    }
}
```

## Recursion Method
* 通过`global values` 记录`maxDeep` and `value` , 然后再进行递归
```java
class Solution {
    int maxDeep = -1;
    int value = 0;
    public int findBottomLeftValue(TreeNode root) {
        value = root.val;
        traversalLeft (root,0);
        return value;
    }
    private void traversalLeft(TreeNode root, int deep){
        if(root == null){
            return ;
        }
        if(root.left == null && root.right == null){
            if(deep> maxDeep){
                 maxDeep = deep;
                 value = root.val;
            }
        }
        if(root.left != null) traversalLeft(root.left, deep + 1);
        if(root.right != null) traversalLeft(root.right, deep + 1);
    }
}
```

***
# 112. Path Sum
* **一刷:24:06(✅)**
* [112. Path Sum](https://leetcode.com/problems/path-sum/description/)

## My Code
* 思路: 通过回溯，每次到底的时候`+`回来；每次往下走的时候`-`去
```java
class Solution {
    public boolean hasPathSum(TreeNode root, int targetSum) {
        if(root == null){
            return false;
        }
        targetSum = targetSum - root.val;
        if(root.left == null && root.right == null){
            if(targetSum == 0){
                return true;
            }
            else {
                targetSum = targetSum + root.val;
                return false;
            }
        }
        boolean left = false;
        boolean right = false;
        if(root.left != null) left = hasPathSum(root.left, targetSum);
        if(root.right != null) right = hasPathSum(root.right,targetSum);
        return left || right;
    }
}
```
***
## 106. Construct Binary Tree from Inorder and Postorder Traversal
* **一刷:70:56(✅)**
* [106. Construct Binary Tree from Inorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/description/)

## My Code
* 思路
  * Inorder顺序:left | in | right; PostOrder : left | right | in ==> 所以通过`postorder`能得到`in`, 通过`Inorder`来划分left 和 right
  * 通过创建两个新数组来记录inLeft和postLeft（因为顺序不一样所以需要分别记录）
```java
class Solution {
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        TreeNode root = new TreeNode();
        if(postorder.length <=0){
            return root;
        }
        int last = postorder.length - 1;
        root.val = postorder[last];
        int left = 0;
        if(last != left){
            for (int i = 0; i <= last ; i ++){
            if(inorder[i] == postorder[last]){
                left = i ;
                break;
            }            
        }}
        if(left > 0){
            int [] arrLeftIn = new int [left];
            int [] arrLeftPo = new int [left];
            for(int i = 0; i < arrLeftIn.length; i ++){
                arrLeftIn[i] = inorder[i];
                arrLeftPo[i] = postorder[i];
            }
            root.left = buildTree(arrLeftIn,arrLeftPo);
            }
        if(last - left > 0){
            int [] arrRightIn = new int [last - left];
            int [] arrRightPo = new int [last - left];
            for(int i = 0; i < arrRightIn.length ; i ++){
                arrRightIn[i] = inorder[left + i + 1];
                arrRightPo[i] = postorder[left + i];    
            }
            root.right = buildTree(arrRightIn,arrRightPo);
        }
        return root;
    }
}
```

## Improvment
* 通过下标来遍历
```java 
class Solution {
    Map<Integer, Integer> map;  // 方便根据数值查找位置
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        map = new HashMap<>();
        for (int i = 0; i < inorder.length; i++) { // 用map保存中序序列的数值对应位置
            map.put(inorder[i], i);
        }

        return findNode(inorder,  0, inorder.length, postorder,0, postorder.length);  // 前闭后开
    }

    public TreeNode findNode(int[] inorder, int inBegin, int inEnd, int[] postorder, int postBegin, int postEnd) {
        // 参数里的范围都是前闭后开
        if (inBegin >= inEnd || postBegin >= postEnd) {  // 不满足左闭右开，说明没有元素，返回空树
            return null;
        }
        int rootIndex = map.get(postorder[postEnd - 1]);  // 找到后序遍历的最后一个元素在中序遍历中的位置
        TreeNode root = new TreeNode(inorder[rootIndex]);  // 构造结点
        int lenOfLeft = rootIndex - inBegin;  // 保存中序左子树个数，用来确定后序数列的个数
        root.left = findNode(inorder, inBegin, rootIndex,
                            postorder, postBegin, postBegin + lenOfLeft);
        root.right = findNode(inorder, rootIndex + 1, inEnd,
                            postorder, postBegin + lenOfLeft, postEnd - 1);

        return root;
    }
}
```

