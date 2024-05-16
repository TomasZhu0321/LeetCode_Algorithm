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
***
#  23. Merge k Sorted Lists
* **一刷:25:22(✅)**
* [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)

## 优化
* 在最开始只传入链表的开头，然后遍历的时候将链表内容再传入priorityqueue能够将时间复杂度减少到O(n*logK)
## My Code
```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) {
            return null;
        }

        // PriorityQueue to keep track of the minimum element from each list
        PriorityQueue<ListNode> pq = new PriorityQueue<>((a, b) -> a.val - b.val);

        // Add the head of each list to the PriorityQueue
        for (ListNode list : lists) {
            if (list != null) {
                pq.add(list);
            }
        }

        // Create a dummy node to form the merged list
        ListNode dummy = new ListNode(-1);
        ListNode current = dummy;

        // While the PriorityQueue is not empty, extract the minimum element and process
        while (!pq.isEmpty()) {
            ListNode node = pq.poll();
            current.next = node;
            current = current.next;

            // If there is a next node in the same list, add it to the PriorityQueue
            if (node.next != null) {
                pq.add(node.next);
            }
        }
        return dummy.next;
    }
}
```

***
#  1086. High Five
* **一刷:25:22(❌)**
* [1086. High Five](https://leetcode.com/problems/high-five/)
## Code 
* 思路
  * 通过Arrays.sort()进行sort之后(TC：Nlog(N))
  * 通过while循环，取前5个，放入的`List<int []>`中
  * 最后取出来的方式
```java
        int[][] solutionArray = new int[solution.size()][];
        return solution.toArray(solutionArray);
```
```java
class Solution {
    public int[][] highFive(int[][] items) {
        int K = 5;
        Arrays.sort(
                items,
                (a, b) -> {
                    if (a[0] == b[0])
                        return b[1] - a[1];
                    return a[0] - b[0];
                });
        List<int[]> solution = new ArrayList<>();
        int n = items.length;
        int i = 0;
        while (i < n) {
            int id = items[i][0];
            int sum = 0;
            // obtain total using the top 5 scores
            for (int k = i; k < i + K; k++)
                sum += items[k][1];
            // ignore all the other scores for the same id
            while (i < n && items[i][0] == id)
                i++;
            solution.add(new int[] { id, sum / K });
        }
        int[][] solutionArray = new int[solution.size()][];
        return solution.toArray(solutionArray);
    }
}
```
***
#  88. Merge Sorted Array
* **一刷:15:22(❌)**
* [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)

## 技巧！🌟
* **Interview Tip** : Whenever you're trying to solve an **array** problem **in place**, always consider the possibility of **iterating backwards** instead of forwards through the array. It can completely change the problem, and make it a lot easier.

## Code
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int p = m + n - 1;
        int a = m - 1;
        int b = n - 1;
        while (p >= 0) {
            if (b < 0) {
                break;
            }
            if (a < 0) {
                nums1[p] = nums2[b];
                b--;
            } else {
                if (nums2[b] >= nums1[a]) {
                    nums1[p] = nums2[b];
                    b--;
                } else {
                    nums1[p] = nums1[a];
                    a--;
                }
            }
            p--;
        }
    }
}

