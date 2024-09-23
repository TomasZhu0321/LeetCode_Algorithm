# Things to look out for during the interview
* **Overlapping Intervals**: Clarify with [1,3][3,4] are considered as overlapping intervals.
* Clarify whether an interval of [a,b] strictly follow a < b,

# Corner Case
* No intervals
* Single Interval
* Two Intervals
* Non-overlapping intervals
* An interval totally consumed within another interval
* Duplicate intervals
* Intervals which start right where an interval ends [1,2],[2,3]

# Techniques
## Sort the array of intervals by its starting point
* `Arrays.sort(arr, (a,b) -> Integer.compare(a[0],b[0]));`

## Checking if two intervals overlap
* Be familiar with writing code to check if two intervals overlap.

## Merging two intervals

# LeetCode
* [Intervals](https://www.techinterviewhandbook.org/algorithms/interval/)

