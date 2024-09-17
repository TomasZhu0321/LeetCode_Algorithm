https://leetcode.com/problems/meeting-rooms-ii/description/
# 问题
![image](./img/MeetingRoom2.png)

# 知识点
## 如何自定义比较器？
```java
1.
Arrays.sort(arr, new Comparator<int[]>(){
    public int compare(int []a, int []b){
        return a[0] - b[0];
    }
});
2.
PriorityQueue<Integer> pq = new PriorityQueue<Integer>(new Comparator<Integer>(){
    public int compare(Integer a, Integer b){
        return a - b;
    }
});

```
# Code
```java
class Solution {
    public int minMeetingRooms(int[][] intervals) {
        if(intervals.length == 1) return 1;
        Arrays.sort(intervals, new Comparator<int []> (){
            public int compare(int [] a , int [] b){
                return a[0] - b[0];
            }
        });
        PriorityQueue<Integer> pq = new PriorityQueue<Integer> (new Comparator <Integer> (){
            public int compare(Integer a, Integer b){
                return a - b;
            }
        });
        pq.offer(intervals[0][1]);
        for(int i =1; i < intervals.length; i++){
            if(intervals[i][0] >= pq.peek()){
                pq.poll();
            }
            pq.offer(intervals[i][1]);
        }
        return pq.size();
    }
}
```