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