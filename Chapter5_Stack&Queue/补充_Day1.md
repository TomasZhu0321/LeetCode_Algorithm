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

