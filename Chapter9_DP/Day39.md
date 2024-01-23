# 62. Unique Paths
* **一刷:12：04(✅)**
* [62. Unique Paths](https://leetcode.com/problems/unique-paths/description/)

## My Code
* 注意如果m=1,n=1，初始值为1 （❌） ==> 其实最开始的初始化m=1, n=1 就应该为1

```java
class Solution {
    public int uniquePaths(int m, int n) {
        int [][] dp = new int[m][n];
        dp[0][0] = 0;
        if(m == 1 && n ==1){
            dp[0][0]=1;
        }
        for(int i = 1; i < m; i ++){
            dp[i][0]=1;
        }
        for(int i = 1; i < n; i ++){
            dp[0][i]=1;
        }
        for(int i = 1; i < m; i ++){
            for(int j = 1; j <n; j ++){
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        }
        return dp[m-1][n-1];
    }
}
```

## Improvment
```java
    public static int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];
        //初始化
        for (int i = 0; i < m; i++) {
            dp[i][0] = 1;
        }
        for (int i = 0; i < n; i++) {
            dp[0][i] = 1;
        }

        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = dp[i-1][j]+dp[i][j-1];
            }
        }
        return dp[m-1][n-1];
    }
```
***
# 63. Unique Path II
* **一刷:12：37(✅)**
* [63. Unique Path II](https://leetcode.com/problems/unique-paths-ii/)

## My Code
* 注意，如果在初始化的时候遇到障碍，剩下的内容都是0
```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        int [][] dp = new int [m][n];
        for(int i = 0;i < m; i ++){
            if(obstacleGrid[i][0] != 1){
                dp[i][0] = 1;
            }
            else {
                break;
            }
        }
        for(int i = 0;i < n; i ++){
            if(obstacleGrid[0][i] != 1){
                dp[0][i] = 1;
            }
            else{
                break;
            }
        }
        for(int i = 1; i < m; i ++){
            for (int j = 1; j < n; j ++){
                if(obstacleGrid[i][j] == 1){
                    dp[i][j] = 0;
                }
                else {
                    dp[i][j] = dp[i-1][j] + dp[i][j-1];
                }
            }
        }
        return dp[m-1][n-1];
    }
}
```
