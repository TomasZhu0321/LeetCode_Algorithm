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

  