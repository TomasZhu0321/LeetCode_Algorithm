# Binary Tree
* In-order traversal is insufficiant to uniquely serialize a tree. Pre-order or post-order traversal is also required.

# Binary Search Tree (BST)
* **In-order** traversal of a BST will give all elements in order.==> This is used to validate whether this is a BST tree or not.
* Time Complexity
  * Access/Search/Insert/Remove: O(logN), with the worse senario O(N) when the tree is very skewed (like a Linked List)
  * Solutions: AVL trees maintain the **balance factor** of each node and perform **rotation operations** when necessary to ensure that the height of tree remains at O(logN)
# Corner Cases
* Empty Tree
* Single Node
* Two Nodes
* Very Skewed Tree(like Linked List)

# Common Routines
* Insert Value
* Delete Value
* Count number of nodes in Tree
* Whether a value is in the tree
* Calculate height of the tree
* Binary Search Tree
  * Determine if it is a binary search tree
  * Get Maximum value
  * Get Minimum value

# Techniques
## Use Recursion
* Recursion is the most common approach for traversing trees. When subtree problem can be used to solve the entire problem, try using recursion
* Base case, usually where the node is null

## Traversing by level
* **BFS**

## Summation of Nodes
* summation of nodes along the way,be sure to check whether nodes can be **negative**

# LeetCode
* [tree](https://www.techinterviewhandbook.org/algorithms/tree/)
