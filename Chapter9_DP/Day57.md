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