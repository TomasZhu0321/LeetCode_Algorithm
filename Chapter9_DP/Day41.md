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
# 96. Unique Binary Search Trees
* **一刷:32:45(✅)**
* [96. Unique Binary Search Trees](https://leetcode.com/problems/unique-binary-search-trees/)

## My Code
* 设置`dp[0]=1`和`dp[1]=1`两个点
* 需要将`奇数偶数`分开讨论
```java
class Solution {
    public int numTrees(int n) {
        int [] dp = new int [n + 1];
        dp[0] = 1;
        dp[1] = 1;
        for(int i = 2; i <= n; i ++){
            int index = i;
            if(i%2 == 1){
                while(index > (i/2) + 1){
                index --;
                dp[i] = dp[i] + dp[index]* dp[i- index - 1]* 2;
            }
            dp[i] = dp[i] + dp[i/2]* dp[i/2];
            }
            else{
                while(index > (i/2)){
                index --;
                dp[i] = dp[i] + dp[index]* dp[i- index - 1]* 2;
            }}
        }
        return dp[n];
    }
}
```
## Improvement
* 通过设置一个`j`来模拟移动，增减自动就变化了
```java
class Solution {
    public int numTrees(int n) {
        int [] dp = new int [n + 1];
        dp[0] = 1;
        dp[1] = 1;
        for(int i = 2; i <= n; i ++){
            for(int j = 1; j <= i; j ++){
                dp[i] += dp[j - 1]* dp[i-j];
            }
        }
        return dp[n];
    }
}
```


