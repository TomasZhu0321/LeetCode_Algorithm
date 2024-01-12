# 654. Maximum Binary Tree
* **一刷:19:46(✅)**
* [654. Maximum Binary Tree](https://leetcode.com/problems/maximum-binary-tree/description/)
## My Code
* 每次通过最大值为分界线，分成`leftNums` 和 `rightNums`
```java
class Solution {
    public TreeNode constructMaximumBinaryTree(int[] nums) {
        Map<Integer,Integer> mapRes = new HashMap<>();
        for(int i = 0 ; i < nums.length; i ++){
            mapRes.put(nums[i],i);
        }
        TreeNode root = new TreeNode(findmax(nums));
        int index = mapRes.get(findmax(nums));
        int [] leftNums = new int [index];
        for(int i = 0 ; i < leftNums.length ; i ++){
            leftNums[i] = nums[i];
        }
        int [] rightNums = new int [nums.length - index - 1];
        for (int i = 0 ; i < rightNums.length; i ++){
            rightNums[i] = nums[index + i + 1];
        }
        if(leftNums.length > 0){
            root.left = constructMaximumBinaryTree(leftNums);
        }
        if(rightNums.length > 0){
            root.right = constructMaximumBinaryTree(rightNums);
        }

        return root;
    }
    private int findmax(int [] nums){
        int max = Integer.MIN_VALUE;
        for(int i : nums){
            if (i > max){
                max = i;
            }
        }
        return max;
    }
}
```
## Improvment
* 通过下标的移动不用每次都开辟新的数组
* 注意`左闭右闭`，在最开始判断的时候`left<right` 才是 null, ==0的时候其实是他本身，还是有值的
```java
class Solution {
    public TreeNode constructMaximumBinaryTree(int[] nums) {
        return conBinaryTree(nums, 0 , nums.length - 1);
    }
    private TreeNode conBinaryTree(int [] nums, int leftIndex ,int rightIndex){
        if(rightIndex - leftIndex < 0){
            return null;
        }
        int maxIndex = leftIndex;
        int max = nums[maxIndex];
        for(int i = leftIndex; i <= rightIndex ;  i ++){
            if(nums[i] > max ){
                max = nums[i];
                maxIndex = i;
            }
        }
        TreeNode root = new TreeNode(max);
        root.left = conBinaryTree(nums, leftIndex, maxIndex - 1);
        root.right = conBinaryTree(nums, maxIndex + 1, rightIndex);
        return root;
    }
}
```

# 617. Merge Two Binary Trees
* **一刷:36:18(❌)**
* [617. Merge Two Binary Trees](https://leetcode.com/problems/merge-two-binary-trees/description/)

## My Questions And Code
### Q1:如果两个tree都为null，那么该如何赋值？
### Q2:如果一边遍历，一边构建TreeNode？

```java
class Solution {
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        Queue <TreeNode> que1 = new LinkedList<>();
        Queue<TreeNode> que2 = new LinkedList<>();
        que1.offer(root1);
        que2.offer(root2);
        Queue<TreeNode> res = new LinkedList<>();
        while(!que1.isEmpty() && !que2.isEmpty()){
            int size1 = que1.size();
            int size2 = que2.size();
            while(size1> 0 || size2> 0){
                TreeNode tmp1 = que1.poll();
                size1 --;
                if(tmp1 != null){
                    que1.offer(tmp1.left);
                    que1.offer(tmp1.right);
                }
                TreeNode tmp2 = que2.poll();
                if(tmp2 != null){
                    que2.offer(tmp2.left);
                    que2.offer(tmp2.right);
                }
                size2 --;
                if(tmp1!= null && tmp2!= null){
                    TreeNode res1 = new TreeNode(tmp1.val + tmp2.val);
                    res.offer(res1);
                }
                if(tmp1 == null && tmp2 != null){
                    TreeNode res1 = new TreeNode(tmp2.val);
                    res.offer(res1);
                }
                if(tmp1!=null && tmp2 == null){
                    TreeNode res1 = new TreeNode(tmp1.val);
                    res.offer(res1);
                }
                if(tmp1 == null && tmp2 == null){
                    res.offer(null);
                }
            }
        }
         if (res == null || res.isEmpty()) {
            return null;
        }

        TreeNode root = res.poll(); // 获取队列的头部元素作为树的根

        Queue<TreeNode> children = new LinkedList<>();

        children.add(root);

        while (!res.isEmpty()) {
            TreeNode current = children.poll(); // 父节点

            // 添加左子节点
            if (!res.isEmpty()) {
                current.left = res.poll(); // 将队列的下一个节点作为左子节点
                children.add(current.left);
            }

            // 添加右子节点
            if (!res.isEmpty()) {
                current.right = res.poll(); // 将队列的下一个节点作为右子节点
                children.add(current.right);
            }
        }
        return root;
    }
}
```
## Keypoints
*  root1和root2传入进来的其实都是address，也就是说可以对他本身进行操作！！
*  如果两边都是`null`，那么直接不操作就好了
```java
* Iteration Method
class Solution {
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        if(root1 == null) return root2;
        if(root2 == null) return root1;
        Queue<TreeNode> que = new LinkedList<>();
        que.offer(root1);
        que.offer(root2);
        while(!que.isEmpty()){
            TreeNode tmp1 = que.poll();
            TreeNode tmp2 = que.poll();
            tmp1.val = tmp1.val + tmp2.val;
            if(tmp1.left != null && tmp2.left !=null){
                que.offer(tmp1.left);
                que.offer(tmp2.left);
            }
            if(tmp1.right != null && tmp2.right != null){
                que.offer(tmp1.right);
                que.offer(tmp2.right);
            }
            if(tmp1.left ==null && tmp2.left != null){
                tmp1.left = tmp2.left;
            }
            if(tmp1.right == null && tmp2.right != null){
                tmp1.right = tmp2.right;
            }
        }
        return root1;
    }
}
```
```java
* Recursion method
class Solution {
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        if(root1 == null) return root2;
        if(root2 == null) return root1;
        root1.val = root1.val + root2.val;
        root1.left = mergeTrees(root1.left, root2.left);
        root1.right = mergeTrees(root1.right,root2.right);
        return root1;
    }
}
```


