# 692. Top K Frequent Words
* **一刷:36:50(✅)**
* [692. Top K Frequent Words](https://leetcode.com/problems/top-k-frequent-words/)

## 知识点
* Comparator比较器问题
  * 如果想 a在b的前面，就 a - b = -1; 如果想 b 在 a的前面，就 a - b = 1;
  * custom比较器其实是让你把谁在前谁在后说明，他肯定还是要返回 -1 ， 1的，只不过是谁减谁返回-1
* String的比较: `b.compareTo(a) //倒序` `a.compareTo(b) //升序` 
* Collections.reverse(list)反转链表

## My Code
```java
class Solution {
    public List<String> topKFrequent(String[] words, int k) {
        Map<String, Integer> map = new HashMap<>();
        for (int i = 0; i < words.length; i++) {
            int num = map.getOrDefault(words[i], 0);
            num++;
            map.put(words[i], num);
        }
        PriorityQueue<String> pq = new PriorityQueue<>((a, b) -> {
            if (map.get(a) == map.get(b)) {
                int res = compare(a, b);
                return res;
            }
            return map.get(a) - map.get(b);
        });

        for(Map.Entry<String,Integer> m: map.entrySet()){
            String key = m.getKey();
            if (pq.size() == k) {
                pq.offer(key);
                pq.poll();
            } else if (pq.size() < k) {
                pq.offer(key);
            }
        }
        String [] r = new String [k];
        for (int i = k - 1; i >= 0; i --) {
            r[i] = pq.poll();
        }
        return Arrays.asList(r);
    }

    private int compare(String a, String b) {
        char[] aArr = a.toCharArray();
        char[] bArr = b.toCharArray();
        int index1 = 0;
        int index2 = 0;
        while (index1 < a.length() && index2 < b.length()) {
            if (aArr[index1] < bArr[index2]) {
                return 1;
            } else if (aArr[index1] > bArr[index2]) {
                return -1;
            } else {
                index1++;
                index2++;
            }
            if (index1 == a.length()) {
                return 1;
            }
            if (index2 == b.length()) {
                return -1;
            }
        }
        return 0;
    }
}
```

## 使用内部函数后的code
```java
class Solution {
    public List<String> topKFrequent(String[] words, int k) {
        Map<String, Integer> cnt = new HashMap<>();
        for (String word : words) {
            cnt.put(word, cnt.getOrDefault(word, 0) + 1);
        }
        PriorityQueue<String> h = new PriorityQueue<>(
                (w1, w2) -> cnt.get(w1).equals(cnt.get(w2)) ? w2.compareTo(w1) : cnt.get(w1) - cnt.get(w2));

        for (String word : cnt.keySet()) {
            h.offer(word);
            if (h.size() > k) {
                h.poll();
            }
        }

        List<String> res = new ArrayList<>();
        while (!h.isEmpty()) {
            res.add(h.poll());
        }
        Collections.reverse(res);
        return res;
    }
}
```
***
# 378. Kth Smallest Element in a Sorted Matrix
* **一刷:30:50(✅)**
* [378. Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/)
## 技巧
### 1.自定义存储node以及初始化方法
```java
class Node {
    int value;
    int row;
    int col;
    public Node(int value, int row, int col){
        this.value = value;
        this.row = row;
        this.col = col;
    }
    public int getValue(){
        return this.value;
    }
    public int getRow(){
        return this.row;
    }
    public int getCol(){
        return this.col;
    }
}
```
### 2. PriorityQueue能够初始化空间
```java
 PriorityQueue<Node> pq = new PriorityQueue<>(Math.min(n,k), (a,b)->{
            return a.getValue() - b.getValue();
        });
```

## Code
```java
class Node {
    int value;
    int row;
    int col;
    public Node(int value, int row, int col){
        this.value = value;
        this.row = row;
        this.col = col;
    }
    public int getValue(){
        return this.value;
    }
    public int getRow(){
        return this.row;
    }
    public int getCol(){
        return this.col;
    }
}
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int n = matrix.length;
        PriorityQueue<Node> pq = new PriorityQueue<>(Math.min(n,k), (a,b)->{
            return a.getValue() - b.getValue();
        });
        //initialize pq
        for(int i = 0 ; i < Math.min(n,k); i ++){
            pq.offer(new Node(matrix[i][0],i,0));
        }
        Node small = pq.peek();
        while(k > 0){
            small = pq.poll();
            int r = small.getRow();
            int c = small.getCol();
            if( c < n - 1){
                pq.offer(new Node(matrix[r][c + 1], r, c + 1));
            }
            k --;
        }
        return small.getValue();
    }
}
```
***
# 767. Reorganize String
* **一刷:60:50(❌)**
* [767. Reorganize String](https://leetcode.com/problems/reorganize-string/)

## 知识点
* **int --> Character** : `Character ch = (char)(i + 'a');`

## Code
### 思路
* 通过MaxHeap来维护char的出现频率
* 分情况讨论
  * 情况1: 取的值(poll) 和之前的结果不一样，直接append
  * 情况2: 和之前结果一样，再取第二顺位(如果没有第二顺位说明走到了死胡同就reutrn “")
```java
class Solution {
    public String reorganizeString(String s) {
        char [] cArr = s.toCharArray();
        int [] alpha = new int [26];
        for(char c : cArr){
            alpha[c - 'a'] ++;
        }
        PriorityQueue<Character> pq = new PriorityQueue<>((a,b)->{
           return  alpha[b - 'a'] - alpha[a - 'a'];
        });
        for(int i = 0 ; i < 26; i ++){
            if(alpha[i]!=0){
                Character cha = (char) (i + 'a');
                pq.offer(cha);
            }
        }
        StringBuilder sb = new StringBuilder();
        while(!pq.isEmpty()){
            char tmp = pq.poll();
            if(sb.length() == 0 || tmp != sb.charAt(sb.length() - 1) ){
                sb.append(tmp);
                alpha[tmp - 'a'] --;
                if(alpha[tmp - 'a'] > 0){
                    pq.offer(tmp);
                }
            }else{
                if(pq.isEmpty()) return  "";
                char tmp2 = pq.poll();
                sb.append(tmp2);
                alpha[tmp2 - 'a'] -- ;
                if(alpha[tmp2 - 'a'] > 0){
                    pq.offer(tmp2);
                }
                pq.offer(tmp);
            }
        }
        return sb.toString();
    }
}
```
***
# 1438. Longest Continuous Subarray With Absolute Diff Less Than or Equal to Limit 
* **一刷:60:50(❌)**
* [1438. Longest Continuous Subarray With Absolute Diff Less Than or Equal to Limit ](https://leetcode.com/problems/longest-continuous-subarray-with-absolute-diff-less-than-or-equal-to-limit/)
## My Code
```java
class Solution {
    public int longestSubarray(int[] nums, int limit) {
        int start = 0, end = 0, res = 0;
        Deque<Integer> maxQue = new LinkedList<>();
        Deque<Integer> minQue = new LinkedList<>();
        while (end < nums.length) {
            // maintain the max inside currnet window: 54321
            if (!maxQue.isEmpty() && nums[maxQue.peekLast()] <= nums[end]) {
                maxQue.pollLast();
            }
            maxQue.offerLast(end);
            // maintain the min inside currnet window: 12345
            if (!minQue.isEmpty() && nums[minQue.peekLast()] >= nums[end]) {
                minQue.pollLast();
            }
            minQue.offerLast(end);
            while (!minQue.isEmpty() && !maxQue.isEmpty()
                    && Math.abs(nums[maxQue.peekFirst()] - nums[minQue.peekFirst()]) > limit) {
                start++;
                if (maxQue.peekFirst() < start) {
                    maxQue.pollFirst();
                }
                if (minQue.peekFirst() < start) {
                    minQue.pollFirst();
                }

            }
            res = Math.max(res, end - start + 1);
            end++;
        }
        return res;
    }
}
```
***
# 295. Find Median from Data Stream
* **一刷:36:50(❌)**
* [295. Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)

## Insight
* 为了保持两个 heap 始终**均分**; 以及各自拥有 **最小/最大** 的两半
  * 将传入值传入maxH / minH中，然后弹出poll，这样就能获得排序好heap中最 小/大值， 然后放入另一半之中！ 
## Code 
```java
class MedianFinder {
    PriorityQueue<Integer> minH = new PriorityQueue<>(1);
    PriorityQueue<Integer> maxH = new PriorityQueue<>(1, (a, b) -> {
        return b - a;
    });
    boolean even = true;

    public MedianFinder() {

    }

    public void addNum(int num) {
        if (even) {
            minH.offer(num);
            maxH.offer(minH.poll());
        } else {
            maxH.offer(num);
            minH.offer(maxH.poll());
        }
        even = !even;
    }

    public double findMedian() {
        double res;
        if (even) {
            res = (minH.peek() + maxH.peek()) / 2.0;
        } else {
            res = maxH.peek() / 1.0;
        }
        return res;
    }
}
```