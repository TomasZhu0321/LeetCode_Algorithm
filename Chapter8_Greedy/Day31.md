# 455. Assign Cookies
* **一刷:15:38(✅)**
* [455. Assign Cookies](https://leetcode.com/problems/assign-cookies/description/)

## My Code
* 思路：通过两个for，其中size的循环通过在外部设置一个j来记录
```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        int res = 0;
        Arrays.sort(g);
        Arrays.sort(s);
        int j = 0;
        for(int i = 0; i < g.length ; i ++){
            for(; j < s.length; j ++){
                if(s[j]>=g[i]) {
                    res ++;
                    j ++;
                    break;
                }
            }
        }
        return res;
    }
}
```

## Improvment
* 通过一个for循环搞定
  * 注意的是，饼干一定是需要遍历完成的 ===> for移动的是饼干
  * 通过外设一个`start=0`来移动孩子
```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        int res = 0;
        Arrays.sort(g);
        Arrays.sort(s);
        int start = 0;
        for(int i = 0; i < s.length && start < g.length; i ++){
            if(g[start] <= s[i]){
                start ++;
                res ++;
            }
        }
        return res;
    }
}
```
***
# 376. Wiggle Subsequence
* **一刷：30:00 （❌）**
* [376. Wiggle Subsequence](https://leetcode.com/problems/wiggle-subsequence/description/)

## Questions
### 1. 如何找到最优结果？
### 2. cur = pre 的更新 为什么不可以放在if外？
![image](https://github.com/TomasZhu0321/LeetCode_Algorithm/blob/main/Chapter8_Greedy/img/376.png)

## Idea
* 通过画图，找到正负变化的点，转折点就是最优数量
* 有三种情况需要讨论
  * 情况1: 单调
  * 情况2: 遇到平坡
  * 情况3: 单调+平坡 (这个情况对应了为什么需要将`cur = pre`放在if之中，因为单调+平坡看似变化了(-/+ ==> 0)但是实际总体还是单调)
    * 因此只有当res ++, 也就是记录了真实的正负交替才更新pre的值
## Code 
```java
class Solution {
    public int wiggleMaxLength(int[] nums) {
        int res = 1;
        if(nums.length == 1){
            return res;
        }
        int pre = 0; 
        for(int i = 0; i < nums.length - 1; i ++){
            int cur = 0;
            if(nums[i + 1] - nums[i] < 0 ){
                cur = -1;
            }
            else if(nums[i + 1] - nums[i] == 0){
                cur = 0;
            }
            else {cur = 1;}
            if(cur != pre && cur != 0) {
                res ++;
                pre = cur;               
            }
        }
        return res;
    }
}
```
***
# 53. Maximum Subarray
* **一刷:18:10(✅)**
* [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/description/)

## 思路
* 通过一个数组，记录`当前值`和`与前一个最大值相加`比较之下的`最大值`
* ![image](https://github.com/TomasZhu0321/LeetCode_Algorithm/blob/main/Chapter8_Greedy/img/53.jpg)
