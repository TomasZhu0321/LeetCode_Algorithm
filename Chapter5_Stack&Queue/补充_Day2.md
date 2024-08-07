# 150. Evaluate Reverse Polish Notation
* **一刷:15：04(✅)**
* [150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

## My Code
```java
class Solution {
    public int evalRPN(String[] tokens) {
        Deque<String> stack = new LinkedList<>();
        for (int i = 0; i < tokens.length; i++) {
            if (tokens[i].equals("+")) {
                String a = stack.pop();
                String b = stack.pop();
                int c = Integer.valueOf(a) + Integer.valueOf(b);
                stack.push(Integer.toString(c));
            } else if (tokens[i].equals("/")) {
                String a = stack.pop();
                String b = stack.pop();
                int c = Integer.valueOf(b) / Integer.valueOf(a);
                stack.push(Integer.toString(c));
            } else if (tokens[i].equals("*")) {
                String a = stack.pop();
                String b = stack.pop();
                int c = Integer.valueOf(b) * Integer.valueOf(a);
                stack.push(Integer.toString(c));
            } else if (tokens[i].equals("-")) {
                String a = stack.pop();
                String b = stack.pop();
                int c = Integer.valueOf(b) - Integer.valueOf(a);
                stack.push(Integer.toString(c));
            } else {
                stack.push(tokens[i]);
            }
        }
        String res = stack.pop();
        return Integer.valueOf(res);
    }
}
```
***
# 224. Basic Calculator
* **一刷:60：04(❌)**
* [224. Basic Calculator](https://leetcode.com/problems/basic-calculator/)

## 知识点
* 判断char是否是一个数字: `Character.isDigit(c);`

## 思路
* 本题首先要理解Parenthesis是改变计算顺序的关键，`stack在这里是用来记录之前的res的 !!`
* 通过`int sign`来记录 `+/-`
* 通过num来记录digit.`num = c + num * 10;` //这里num x 10是因为以防是很多位数字 **(很巧妙！)**
* 然后pop进去的sign不是之前res的sign，而是括号前的sign，所以取出的时候是`sign * 括号内的res + rTmp;`
* 当遇到 + / - 的时候，更新res的结果，`res = res + num * sign;`. 理解：因为 +/-其实是表明前一个数字结束了，他记录的也是前一个num和num前的sign不是当前的！！！

## Code 
```java
class Solution {
    public int calculate(String s) {
        int num = 0;
        int res = 0;
        int sign = 1;
        Deque<Integer> stack = new LinkedList<>();
        for (char c : s.toCharArray()) {
            if (Character.isDigit(c)) {
                num = num * 10 + c - '0';
            } else if (c == '+' || c == '-') {
                res = res + num * sign;
                num = 0;
                sign = c == '+' ? 1 : -1;
            } else if (c == '(') {
                stack.push(sign);
                stack.push(res);
                res = 0;
                sign = 1;
                num = 0;
            } else if (c == ')') {
                res = res + num * sign;
                int rTmp = stack.pop();
                int sTmp = stack.pop();
                res = rTmp + res * sTmp;
                num = 0;
            }
        }
        if (num != 0) {
            res += num * sign;
        }
        return res;
    }
}
```
***
# 1472. Design Browser History
* **一刷:20：04(❌)**
* [1472. Design Browser History](https://leetcode.com/problems/design-browser-history/)

## My Code
```java
class BrowserHistory {
    private Deque<String> history = new LinkedList<>();
    private Deque<String> future = new LinkedList<>();
    private String current;

    public BrowserHistory(String homepage) {
        // 'homepage' is the first visited URL.
        current = homepage;
    }

    public void visit(String url) {
        // Push 'current' in 'history' stack and mark 'url' as 'current'.
        history.push(current);
        current = url;
        // We need to delete all entries from 'future' stack.
        future = new LinkedList<>();
    }

    public String back(int steps) {
        // Pop elements from 'history' stack, and push elements in 'future' stack.
        while (steps > 0 && !history.isEmpty()) {
            future.push(current);
            current = history.pop();
            steps--;
        }
        return current;
    }

    public String forward(int steps) {
        // Pop elements from 'future' stack, and push elements in 'history' stack.
        while (steps > 0 && !future.isEmpty()) {
            history.push(current);
            current = future.pop();
            steps--;
        }
        return current;
    }
}
```
***
# 1209. Remove All Adjacent Duplicates in String II
* **一刷:30：04(❌)**
* [1209. Remove All Adjacent Duplicates in String II](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string-ii/)

## 知识点
* 对String直接进行删除操作(甚至删除中间) : `sb.delete(start,end);`
## 思路
* 通过stack来记录的总数，然后直接通过StringBuilder进行删减操作
* stack记录的是总数，所以不用1，2，3，单个相加！
* 当删除操作过后，需要进行**回退**！！！ `i = i - k;`
* 每次开头都需要判断`sb.charAt(i) != sb.charAt(i - 1)`，这样也保证了落下来的新东西是否能够继续消消乐

## Code
```java
class Solution {
    public String removeDuplicates(String s, int k) {
        Deque<Integer> counts = new LinkedList<>();
        StringBuilder sb = new StringBuilder(s);
        for(int i = 0 ; i < sb.length(); i ++){
            if(i == 0  || sb.charAt(i) != sb.charAt(i - 1)){
                counts.push(1);
            }
            else{
                int increments = counts.pop() ;
                increments ++;
                if(increments == k){
                    sb.delete(i - k + 1, i + 1);
                    i = i - k;
                }else{
                    counts.push(increments);
                }
            }
        }
        return sb.toString();
    }
}
```
***
# 1249. Minimum Remove to Make Valid Parenthese
* **一刷:30：04(✅)**
* [1249. Minimum Remove to Make Valid Parenthese](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/)

## My Code
* Stack与其他类型结合的问题，可以通过Stack来记录index

```java
class Solution {
    public String minRemoveToMakeValid(String s) {
        Deque<Integer> indexs = new LinkedList<>();
        char[] sb = s.toCharArray();
        for (int i = 0; i < sb.length; i++) {
            if (!Character.isLowerCase(sb[i])) {
                if (sb[i] == ')') {
                    if (indexs.isEmpty() || sb[indexs.peek()] == ')') {
                        sb[i] = ' ';
                    } else if (sb[indexs.peek()] == '(') {
                        indexs.pop();
                    }
                } else if (sb[i] == '(') {
                    if (indexs.isEmpty() || sb[indexs.peek()] == '(') {
                        indexs.push(i);
                    }
                }
            }
        }
        while (!indexs.isEmpty()) {
            int x = indexs.pop();
            sb[x] = ' ';
        }
        StringBuilder res = new StringBuilder();
        for (int i = 0; i < sb.length; i++) {
            if (sb[i] != ' ') {
                res.append(String.valueOf(sb[i]));
            }
        }
        return res.toString();
    }
}
```
***
# 735. Asteroid Collision
* **一刷:20：04(✅)**
* [735. Asteroid Collision](https://leetcode.com/problems/asteroid-collision/)
## 知识点
* 栈的时间复杂度问题：因为不是对整个stack中的元素进行操作，那么就是O(N)

```java
class Solution {
    public int[] asteroidCollision(int[] asteroids) {
        Deque<Integer> stack = new LinkedList<>();
        for (int i = 0; i < asteroids.length; i++) {
            if (!stack.isEmpty() && asteroids[i] < 0 && stack.peek() > 0) {
                int tmp = stack.pop();
                if (Math.abs(tmp) == Math.abs(asteroids[i]))
                    continue;
                int res = Math.max(Math.abs(tmp), Math.abs(asteroids[i])) == Math.abs(tmp) ? tmp : asteroids[i];
                while (!stack.isEmpty() && res < 0 && stack.peek() > 0) {
                    tmp = stack.pop();
                    if (Math.abs(tmp) == Math.abs(asteroids[i]))
                        break;
                    res = Math.max(Math.abs(tmp), Math.abs(asteroids[i])) == Math.abs(tmp) ? tmp : asteroids[i];
                }
                if (Math.abs(tmp) != Math.abs(asteroids[i])) {
                    stack.push(res);
                }
            } else {
                stack.push(asteroids[i]);
            }
        }
        int[] arr = new int[stack.size()];
        for (int i = stack.size() - 1; i >= 0; i--) {
            arr[i] = stack.pop();
        }
        return arr;
    }
}
```