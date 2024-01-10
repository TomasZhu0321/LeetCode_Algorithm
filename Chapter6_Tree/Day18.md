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
