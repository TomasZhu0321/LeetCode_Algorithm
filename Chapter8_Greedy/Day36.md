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
