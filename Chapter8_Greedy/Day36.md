# 435. Non-overlapping Intervals
* **一刷:15:49(✅)**
* [435. Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/)

## My Code
```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        int min = intervals[0][1];
        int res = 0;
        for (int i = 1; i < intervals.length; i++) {
            int curEnd = intervals[i][1];
            int curStart = intervals[i][0];
            int preEnd = intervals[i - 1][1];
            if (curStart < min) {
                res++;
                min = Math.min(curEnd, min);
            } else {
                min = curEnd;
            }
        }
        return res;
    }
}
```
***
# 763. Partition Labels
* **一刷:30:49(✅)**
* [763. Partition Labels](https://leetcode.com/problems/partition-labels/)

## My Code
```java
class Solution {
    public List<Integer> partitionLabels(String s) {
        int[] letters = new int[26];
        for (int i = 0; i < s.length(); i++) {
            int index = s.charAt(i) - 97;
            letters[index] = i;
        }
        List<Integer> res = new LinkedList<>();
        int start = 0;
        int i = 0;
        while (start < s.length() && i < s.length()) {
            int end = letters[s.charAt(i) - 97];
            while (i < end) {
                if (letters[s.charAt(i) - 97] > end) {
                    end = letters[s.charAt(i) - 97];
                }
                i++;
            }
            res.add(end - start + 1);
            start = end + 1;
            i = start;
        }
        return res;
    }
}
```
***
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
# 56. Merge Intervals
* **一刷:30:49(✅)**
* [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)

## My Code
```java
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        List<int[]> list = new LinkedList<>();
        int start = intervals[0][0];
        int end = intervals[0][1];
        for (int i = 0; i < intervals.length; i++) {
            int[] cur_res = new int[2];
            int cur_start = intervals[i][0];
            int cur_end = intervals[i][1];
            if (cur_start > end) {
                cur_res[0] = start;
                cur_res[1] = end;
                list.add(cur_res);
                start = cur_start;
                end = cur_end;
            } else {
                end = Math.max(end, cur_end);
            }
            if (i == intervals.length - 1) {
                int[] cur_res_last = new int[2];
                cur_res_last[0] = start;
                cur_res_last[1] = end;
                list.add(cur_res_last);
            }
        }

        return list.toArray(new int[list.size()][]);

    }
}
```