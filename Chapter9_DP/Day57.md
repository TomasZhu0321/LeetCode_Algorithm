# 647. Palindromic Substrings
* **一刷:10:50(❌)**
* [647. Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/)

## Code 
```java
class Solution {
    public int countSubstrings(String s) {
        char[] chr = s.toCharArray();
        boolean[][] dp = new boolean[chr.length][chr.length];
        int res = 0;
        for (int i = chr.length - 1; i >= 0; i--) {
            for (int j = i; j < chr.length; j++) {
                if (chr[i] == chr[j]) {
                    if (j - i <= 1) {
                        res++;
                        dp[i][j] = true;
                    } else {
                        if (dp[i + 1][j - 1]) {
                            res++;
                            dp[i][j] = true;
                        }
                    }
                }
            }
        }
        return res;

    }
}
```
***
# 516. Longest Palindromic Subsequence 
* **一刷:60:50(❌)**
* [516. Longest Palindromic Subsequence ](https://leetcode.com/problems/longest-palindromic-subsequence/)

## Code
* 思路:
  * dp中的二维数组的dp[i + 1][j]或者dp[i][j - 1]可以具象的理解为: `只考虑加入s[i]或者s[j]的情况下，值是多少`
* **Palindromic问题**
  * 思路是 **i,从后往前**遍历，这样能够模拟`回文串`的效果
  * 如果遇到相同的，是各退一步，找到都没加入时，dp[i + 1][j - 1]的最大值，然后 + 2
  * 因为直接+2, 最开始单个字母永远可以构成回文，所以每一行开头i = i 时，初始化为1 `dp[i][i] = 1`
```java
class Solution {
    public int longestPalindromeSubseq(String s) {
        char[] chr = s.toCharArray();
        int len = chr.length;
        int[][] dp = new int[len + 1][len + 1];
        for (int i = len - 1; i >= 0; i--) {
            dp[i][i] = 1;
            for (int j = i + 1; j < len; j++) {
                if (chr[i] == chr[j]) {
                    dp[i][j] = dp[i + 1][j - 1] + 2;
                } else {
                    dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
                }

            }
        }
        return dp[0][len - 1];
    }
}
```