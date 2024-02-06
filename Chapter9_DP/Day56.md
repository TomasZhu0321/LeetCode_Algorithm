# 583. Delete Operation for Two Strings
* **一刷:40:50(❌)**
* [583. Delete Operation for Two Strings](https://leetcode.com/problems/delete-operation-for-two-strings/description/)

## 问题
* 当不相同时，其实有`三种`删除的操作
  * 删除当前的 `dp[i - 1][j] + 1`
  * 删除对应的 `dp[i][j - 1] + 1`
  * 删除两个`dp[i - 1][j - 1] + 1`

```java
class Solution {
    public int minDistance(String word1, String word2) {
        int len1 = word1.length();
        int len2 = word2.length();
        int [][] dp = new int [len1 + 1][len2 + 1];
        for (int i = 1; i <= len1 ; i ++){
            dp[i][0] = i;
        }
        for (int i = 1; i <= len2; i ++){
            dp[0][i] = i;
        }
        for(int i = 1; i <= len1; i ++){
            for (int j = 1; j <= len2; j ++){
                if(word1.charAt(i - 1) == word2.charAt(j - 1)){
                    dp[i][j] = dp[i - 1][j - 1];
                }
                else {
                     int tmp1 = dp[i][j - 1]  + 1;
                     int tmp2 = dp[i - 1][j] + 1;
                     int tmp3 = dp[i - 1][j - 1] + 2;
                     int less1 = Math.min(tmp1,tmp2);
                     dp[i][j] = Math.min(less1, tmp3);
                }
            }
        } 
        return dp[len1][len2];   
    }
}
```
## 思路 2: 通过最大子序列问题来求解
[1143. 最长子序列](https://github.com/TomasZhu0321/LeetCode_Algorithm/blob/f7bce2d51cc6012db565f43a273c9a61e0a7ef10/Chapter9_DP/Day53.md)