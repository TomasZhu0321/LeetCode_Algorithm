# 343. Integer Break
* **一刷:28:50(✅)**
* [343. Integer Break](https://leetcode.com/problems/integer-break/description/)

## My Code
* 找准`2`和`3`其实是本身更大。也就是`质数（Prime number）`
* 做题时列举到`n=10`左右，能有大概结果
```java
class Solution {
    public int integerBreak(int n) {
        int [] dp = new int [n - 1];
        dp[0] = 1;
        if(n == 2){
            return dp[n - 2];
        }
        for(int i = 1; i < dp.length; i ++){
            if( i <= 4 ){
                dp[i] = Math.max((i * 2),(i - 1)*3);
            }
            else {
                dp[i] = Math.max(dp[i-2]*2, dp[i-3]*3);
            }
        }
        return dp[n-2];
    }
}
```
