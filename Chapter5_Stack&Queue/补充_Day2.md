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