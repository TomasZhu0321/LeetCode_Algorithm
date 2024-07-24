# 题目
```java
This problem was asked by Google.

Given a list of integers S and a target number k, write a function that returns a subset of S that adds up to k. If such a subset cannot be made, then return null.

Integers can appear more than once in the list. You may assume all numbers in the list are positive.

For example, given S = [12, 1, 61, 5, 9, 2] and k = 24, return [12, 9, 2, 1] since it sums up to 24.
```

## Code
* 背包问题，0-1背包
```java
class Solution{
    public static List<Integer> subsetSum(int [] list, int target){
        int len = list.length;
        int row = len + 1;
        int col = target + 1;
        boolean [][] dp = new boolean[row + 1][col + 1];
        //initialize dp
        for(int i = 0; i < row; i ++){
            dp[i][0] = true;
        }
        //dp
        for(int i = 1; i < row; i ++){
            for(int j = 1; j < col; j ++){
                if(list[i - 1] > j){
                    dp[i][j] = dp[i - 1][j];
                }
                else {
                    dp[i][j] = dp[i - 1][j] || dp[i - 1][j - list[i - 1]];
                }
            }
        }
        if(dp[len][target] == false) {
            return null;
        }
        List<Integer> res = new ArrayList<>();
        int i = len, j = target;
        while(i > 0 && j > 0){
            if(dp[i - 1][j]){
                i --;
            }
            else {
                res.add(list[i - 1]);
                j -= list[i - 1];
                i --;
            }
        }
        return res;
    }

    public static void main(String [] args){
        int [] list = { 12, 1, 61, 5, 9, 2 };
        int k = 22;
        List<Integer> res = subsetSum(list,k);
        if(res!=null){
            System.out.println("It can sum up to the target : " + res);
        }else {
            System.out.println("It cannot sum up to the target");
        }

    }
}
```