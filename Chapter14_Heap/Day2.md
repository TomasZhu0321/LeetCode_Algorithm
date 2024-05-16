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