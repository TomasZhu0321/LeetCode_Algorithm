# 973. K Closest Points to Origin
* **一刷:25:22(✅)**
* [973. K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)
## Code
```java
class Solution {
    public int[][] kClosest(int[][] points, int k) {
        // heap
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> {
            return distance(a[0], a[1]) - distance(b[0], b[1]);
        });
        for (int i = 0; i < points.length; i++) {
            int[] tmp = new int[2];
            tmp[0] = points[i][0];
            tmp[1] = points[i][1];
            pq.add(tmp);
        }
        int[][] res = new int[k][2];
        for (int i = 0; i < k; i++) {
            int[] tmp = pq.poll();
            res[i][0] = tmp[0];
            res[i][1] = tmp[1];
        }
        return res;
    }

    private int distance(int x, int y) {
        return (x * x + y * y);
    }
}
```
***
# 347. Top K Frequent Elements
* **一刷:25:22(✅)**
* [347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)

## 技巧
* `Map.Entry<Integer,Integer> me : map.entrySet()` 来获得一组map的值
* `pq.add(new int []{me.getKey(),me.getValue()});` 来添加结果
* `PriorityQueue<int []> pq = new PriorityQueue<>((pair1,pair2) -> pair1[1] - pair2[1]);` 比较的是value的值
## Code
```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        if(nums.length == k) return nums;
        Map<Integer,Integer> map = new HashMap<>();
        for (int i : nums){
            map.put(i,map.getOrDefault(i,0) + 1);
        }
        PriorityQueue<int []> pq = new PriorityQueue<>((pair1,pair2) -> pair1[1] - pair2[1]);
        for(Map.Entry<Integer,Integer> me : map.entrySet()){
            pq.add(new int []{me.getKey(),me.getValue()});
            if(pq.size() > k){
                pq.poll();
            }
        }
        int [] res = new int [k];
        for(int i =0; i<k;i ++){
            res[i] = pq.poll()[0];
        }
        return res;
    }
}
```