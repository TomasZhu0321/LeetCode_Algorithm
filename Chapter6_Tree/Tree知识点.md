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

# Tree Traversal
Tree traversal refers to the process of visiting each node in a tree exactly once in some order. In binary trees, the most common traversal methods fall into two main categories: `Depth-First Search (DFS)` and `Breadth-First Search (BFS)`. Each traversal method has its unique characteristics and applications.
## Depth-First Search (DFS)
* Depth-First Search tries to explore as **deep** as possible down each branch before backtracking. This type of traversal can be further divided into three main methods: *Pre-order*, *In-order*, and *Post-order* traversal.
![image](https://github.com/TomasZhu0321/LeetCode_Algorithm/blob/main/Chapter6_Tree/img/dfsTraversal.png)

### Pre-order Traversal
* Order of Visiting: Visit the **root** node first, then traverse the **left** subtree, and finally traverse the **right** subtree
* Application: Used for **cloning a tree** structure, as it preserves the structure of the tree

### In-order Traversal
* Order of Visiting: Traverse the **left** subtree first, visit the **root** node, and then traverse the **right** subtree
* Application: In a binary search tree, in-order traversal visits the nodes in **ascending** order, useful for **sorting** and **retrieval** operations.

### Post-order Traversal
* Order of Visiting: Traverse the **left** subtree first, then the **right** subtree, and finally visit the **root** node
* Application: Used in scenarios where children nodes need to be processed before the parent node, such as **deleting** a folder and its contents in a file system.

## Breadth-First Search (BFS)
Breadth-First Search starts at the root node and explores the tree level by level. This type of traversal typically uses a `queue` to facilitate the process

### Level-order Traversal
* Order of Visiting: Start at the root node, then move to the second level, the third level, and so forth, moving level by level downwards.
* Application: Used for **level-related problems**, such as finding the **minimum or maximum depth** of a tree or printing the nodes of a tree level by level.

## Implementation
* `DFS` is typically implemented using **recursion** or a **stack**.
* `BFS` is usually implemented using a **queue** to store the nodes of each level.

# Defination of Tree (Code)
```
pulbic class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;

    TreeNode(){};
    TreeNode (int val){ this.val = val};
    TreeNode (int val, TreeNode left, TreeNode right){
        this.val = val;
        this.left = left;
        this.right = right;
    }
}
```

