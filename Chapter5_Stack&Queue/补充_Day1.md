# 225. Implement Stack using Queues
* **一刷:16：04(✅)**
* [225. Implement Stack using Queues](https://leetcode.com/problems/implement-stack-using-queues/)

## My Code
```java
class MyStack {
    int size;
    Deque<Integer> dq;

    public MyStack() {
        size = 0;
        dq = new LinkedList<>();
    }

    public void push(int x) {
        dq.offer(x);
        size++;
        int time = size - 1;
        while (time != 0) {
            dq.offer(dq.poll());
            time--;
        }
    }

    public int pop() {
        size--;
        return dq.poll();
    }

    public int top() {
        return dq.peek();
    }

    public boolean empty() {
        if (size == 0)
            return true;
        return false;
    }
}
```
***
# 54. Spiral Matrix
* **一刷:27：04(✅)**
* [54. Spiral Matrix](https://leetcode.com/problems/spiral-matrix/)

## My Code
```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> res = new LinkedList<>();
        int row = matrix.length - 1; // 0, 1 ,2
        int col = matrix[0].length - 1; // 0, 1, 2, 3
        int i = 0, j = 0;
        int time = Math.min(row + 1, col + 1) / 2; // 3/2= 1;
        int range = 0;
        while (time > 0) {
            while (j < col - range) {
                res.add(matrix[i][j]);
                j++;
            }
            while (i < row - range) {
                res.add(matrix[i][j]);
                i++;
            }
            while (j > range) {
                res.add(matrix[i][j]);
                j--;
            }
            while (i > range) {
                res.add(matrix[i][j]);
                i--;
            }
            j++;
            i++;
            time--;
            range++;
        }
        if (res.size() != (row + 1) * (col + 1)) {
            int left = (row + 1) * (col + 1) - res.size();
            while (left > 0) {
                if (row == Math.max(row, col)) {
                    res.add(matrix[i][j]);
                    i++;
                } else {
                    res.add(matrix[i][j]);
                    j++;
                }
                left--;
            }
        }
        return res;
    }
}
```
***
# 346. Moving  Average from Data Stream
* **一刷:7：04(✅)**
* [346. Moving  Average from Data Stream](https://leetcode.com/problems/moving-average-from-data-stream/)

## My Code
```java
class MovingAverage {
    int num,sum,size;
    Deque <Integer> dq = new LinkedList<>();
    public MovingAverage(int size) {
        num = 0;
        sum = 0;
        this.size = size;
    }
    public double next(int val) {
        dq.offer(val);
        sum += val;
        num ++;
        if(num > size){
            sum -= dq.poll();
            num --;
        }
        return (double) sum / num;
    }
}
```
***
# 281. Zigzag Iterator
* **一刷:9：04(✅)**
* [281. Zigzag Iterator](https://leetcode.com/problems/zigzag-iterator/)

## My Code
```java
public class ZigzagIterator {
    Deque<Integer> dq = new LinkedList<>();
    int size1, size2;
    public ZigzagIterator(List<Integer> v1, List<Integer> v2) {
        size1 = v1.size();
        size2 = v2.size();
        int index = 0;
        while (size1 != 0 || size2 != 0) {
            if (size1 != 0 && size2 != 0) {
                dq.add(v1.get(index));
                dq.add(v2.get(index));
                size1--;
                size2--;
            } else if (size1 == 0 && size2 != 0) {
                dq.add(v2.get(index));
                size2--;
            } else {
                dq.add(v1.get(index));
                size1--;
            }
            index ++;
        }
    }

    public int next() {
        return dq.poll();
    }

    public boolean hasNext() {
        return !dq.isEmpty();
    }
}
```
***
# 1429. First Unique Numbe
* **一刷:20：04(✅)**
* [1429. First Unique Numbe](https://leetcode.com/problems/first-unique-number/)

## My Code
```java
class FirstUnique {
    Map<Integer, Integer> map = new HashMap<>();
    Deque<Integer> dq = new LinkedList<>();

    public FirstUnique(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            add(nums[i]);
        }
    }
    public int showFirstUnique() {
        if (dq.isEmpty())
            return -1;
        int tmp = dq.peek();
        if (map.get(tmp) == 1) {
            return tmp;
        } else {
            dq.poll();
        }
        return showFirstUnique();
    }

    public void add(int value) {
        int v = map.getOrDefault(value, 0);
        v = v + 1;
        map.put(value, v);
        if (v == 1) {
            dq.offer(value);
        }
    }
}
```
***
# 362. 362. Design Hit Counter
* **一刷:60：04(❌)**
* [362. 362. Design Hit Counter](https://leetcode.com/problems/design-hit-counter/) 

## My Code
```java
class HitCounter {
    private Deque<Integer> hits = new LinkedList<Integer>();

    public HitCounter() {
    }
    public void hit(int timestamp) {
        this.hits.add(timestamp);
    }
    
    public int getHits(int timestamp) {
        while (!hits.isEmpty()) {
            int diff = timestamp - hits.peek();
            if (diff >= 300) hits.poll();
            else break;
        }
        return hits.size();
    }
}
```
***
# 155. Min Stack
* **一刷:15：04(✅)**
* [155. Min Stack](https://leetcode.com/problems/min-stack/) 

## My Code
```java
class MinStack {
    int min = Integer.MAX_VALUE;
    Deque<Integer> stack = new LinkedList<>();
    Deque<Integer> minStack = new LinkedList<>();

    public MinStack() {

    }

    public void push(int val) {
        if (minStack.isEmpty()) {
            minStack.push(val);
        } else {
            int peek = minStack.peek();
            minStack.push(Math.min(peek, val));
        }
        stack.push(val);
    }

    public void pop() {
        stack.pop();
        minStack.pop();
    }

    public int top() {
        return stack.peek();
    }

    public int getMin() {
        return minStack.peek();
    }
}
```