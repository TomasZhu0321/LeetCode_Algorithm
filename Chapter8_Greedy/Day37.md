# 76. Minimum Window Substring
* **一刷:50:49(❌)**
* [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)

## 代码技巧
### ASCII 码一共 128
* 可以直接通过 `int [128]`分配的数组来将所有ascii码归纳进去(A-Z,a-z)
* `arr['A'],arr['a']`能够直接在对应char位置记录个数等
### 操作String
* `char [] t_arr = t.toCharArray();`需要对字符串里面单个char操作时，可以直接用char来

## 本题解题思路
* 通过**count记录总的个数**
  * 这样可以判断count == t.length时，说明就找到了对应的一个substring
* 通过while里面再while，**R来控制右边界，L来控制左边界** 实现窗口滑动
```java
class Solution {
    public String minWindow(String s, String t) {
        char[] s_arr = s.toCharArray();
        char[] t_arr = t.toCharArray();
        int[] arr = new int[128];
        for (char i : t_arr) {
            arr[i]++;
        }
        int count = 0;
        int L = 0;
        int R = 0;
        int minLen = Integer.MAX_VALUE;
        String res = "";
        while (R < s_arr.length) {
            char tmp = s_arr[R];
            arr[tmp]--;
            if (arr[tmp] >= 0) {
                count++;
            }
            while (count == t_arr.length) {
                int len = R - L + 1;
                if (len < minLen) {
                    minLen = len;
                    res = s.substring(L, R + 1);
                }
                arr[s_arr[L]]++;
                if (arr[s_arr[L]] > 0) {
                    count--;
                }
                L++;
            }
            R++;
        }
        return res;

    }
}
```
***
# 738. Monotone Increasing Digits
* **一刷:50:49(❌)**
* [738. Monotone Increasing Digits](https://leetcode.com/problems/monotone-increasing-digits/)

## 代码技巧
* Integet ==> String: `Integer.toString(n)`;
* char [] chr ==> String: `new String(chr)`;
* char 的数字 可以直接+,- 

## 思路
* 通过记录一个起始值，这个值以及之后全部变成9就可以(因为要求递增，最后都是9了，那之前必须比他小才可以)
```java
class Solution {
    public int monotoneIncreasingDigits(int n) {
        if (n < 10)
            return n;
        String str = Integer.toString(n);
        char[] chr = str.toCharArray();
        int start = chr.length;
        for(int i = chr.length - 1; i > 0 ; i --){
            if(chr[i - 1] > chr[i]){
                start = i;
                chr[i - 1] --;
            }
        }
        for(int i = start; i < chr.length; i ++){
            chr[i] = '9';
        }
        return Integer.parseInt(new String(chr));
    }
}
```