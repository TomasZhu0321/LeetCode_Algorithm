# Tree的种类
## Full Binary Tree
* Each node has either no children or two children
* In a full binary tree, all leaves are at the same level
* For a full binary tree with `'L'` levels, the totoal number of nodes is `2<sub>L</sub>-1`
![image](https://github.com/TomasZhu0321/LeetCode_Algorithm/blob/main/Chapter6_Tree/img/fullBinary.png)

## Complete Binary Tree
* All levels are completely filled except possibly the last level
* At the last level, all nodes are as far `left` as possible
* A complete binary tree does not necessarily have to be full, but a full binary tree is always complete
![image](https://github.com/TomasZhu0321/LeetCode_Algorithm/blob/main/Chapter6_Tree/img/completeBinary.png)

## Binary Search Tree(BST)
* Each node's left subtree contains only values less than the node's value, and the right subtree only values greater
* BSTs allow for efficient data `searching`, `insertion`, and `deletion`

![image](https://github.com/TomasZhu0321/LeetCode_Algorithm/blob/main/Chapter6_Tree/img/BST.png)

## Balanced Binary Search Tree
* A special kind of BST where the height difference between the left and right subtree for every node is `at most 1`
* AVL Tree is a common type of balanced binary search tree, which maintains tree balance through rotations
* Ensures that the time complexity for search, insertion, and deletion operations remains `O(log n)` in the worst-case scenario
![image](https://github.com/TomasZhu0321/LeetCode_Algorithm/blob/main/Chapter6_Tree/img/BBST.png)