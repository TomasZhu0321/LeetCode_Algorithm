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
