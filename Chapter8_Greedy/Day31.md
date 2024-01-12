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
