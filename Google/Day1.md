# Google 代码规范
* 1. 缩进是2 spaces
* 2. 注释空一行
* 3. 每个方法前简要描述功能
* 4. if/else/while语句都是前后有空格

# 959. Regions Cut By Slashed
* **一刷:30:22(❌)**
* [959. Regions Cut By Slashed](https://leetcode.com/problems/regions-cut-by-slashes/?envType=company&envId=google&favoriteSlug=google-thirty-days&difficulty=MEDIUM)

## 思路
* 将一个cell看作是四个vertices的方格，通过Disjoint Union Set data structure，找到connected edges
* 初始值boundry都连在一起
* TC: O(N^2 * a(n^2)), where a is inverse Ackermann function
* SC: O(N^2)
## Code
```java
class Solution {
  /**
   * Solution class to solve the problem of counting regions by slashes.
   * The algorithm uses the Disjoint Set Union (DSU) data structure to count
   * the number of regions formed by slashes in the grid.
   */
  public int regionsBySlashes(String[] grid) {
    // Initialize DSU data structure
    int gridSize = grid.length;
    int pointsPerSide = gridSize + 1;
    int totalPoints = pointsPerSide * pointsPerSide;
    int[] parentArray = new int[totalPoints];
    Arrays.fill(parentArray, -1);

    // Connect boundary points
    for (int i = 0; i < pointsPerSide; i++) {
      for (int j = 0; j < pointsPerSide; j++) {
        if (i == 0 || j == 0 || i == pointsPerSide - 1 || j == pointsPerSide - 1) {
          int coord = i * pointsPerSide + j;
          parentArray[coord] = 0;
        }
      }
    }

    // Set top-left point to -1
    parentArray[0] = -1;
    int regionCount = 1;

    // Process each cell in the grid
    for (int i = 0; i < gridSize; i++) {
      for (int j = 0; j < gridSize; j++) {
        if (grid[i].charAt(j) == '/') {
          int topRight = i * pointsPerSide + (j + 1);
          int downLeft = (i + 1) * pointsPerSide + j;
          regionCount += union(parentArray, topRight, downLeft);
        } else if (grid[i].charAt(j) == '\\') {
          int topLeft = i * pointsPerSide + j;
          int downRight = (i + 1) * pointsPerSide + (j + 1);
          regionCount += union(parentArray, topLeft, downRight);
        }
      }
    }

    return regionCount;
  }

  /**
   * Finds the root of the set containing the given node.
   *
   * @param parentArray the DSU array representing the sets
   * @param node the node to find
   * @return the root of the set containing the node
   */
  private int find(int[] parentArray, int node) {
    if (parentArray[node] == -1) {
      return node;
    }

    // Path Compression, reduce time complexity to amortized time complexity O(a(n))
    parentArray[node] = find(parentArray, parentArray[node]);
    return parentArray[node];
  }

  /**
   * Unions two sets containing the given nodes and returns 1 if a new region
   * is formed, 0 otherwise.
   *
   * @param parentArray the DSU array representing the sets
   * @param node1 the first node
   * @param node2 the second node
   * @return 1 if a new region is formed, 0 otherwise
   */
  private int union(int[] parentArray, int node1, int node2) {
    int parent1 = find(parentArray, node1);
    int parent2 = find(parentArray, node2);

    // Nodes are already in the same set, new region formed
    if (parent1 == parent2) {
      return 1;
    }

    // Union the sets
    parentArray[parent2] = parent1;
    return 0;
  }
}
```

