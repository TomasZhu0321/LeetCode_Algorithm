# 20. Valid Parentheses
* **一刷:52：04(✅)**
* [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

## My Code
* 需要考虑`return false`的三种情况
  * stack跳出的与当前的不匹配
  * 最后stack有剩余
  * 当前stack为empty，但想放入` ]/)/} ` (也就是没有开头就放入结尾)
```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        for(int i = 0; i < s.length(); i ++){
            if(s.charAt(i) == '('){
                stack.push(')');
            }
            else if( s.charAt(i) == '['){
                stack.push(']');
            }
            else if(s.charAt(i) == '{'){
                stack.push('}');
            }
            else{
                if(stack.isEmpty()){
                    return false;
                }
                char tmp = stack.pop();
                if(tmp != s.charAt(i)){
                    return false;
                }
            }
        }
        return stack.isEmpty();
    }
}
```
***
# 1047. Remove All Adjacent Duplicates In String
* **一刷:08:37(✅)**
* [1047. Remove All Adjacent Duplicates In String](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)
## My Code
```java
class Solution {
    public String removeDuplicates(String s) {
        Stack<Character> stack = new Stack<>();
        stack.push(s.charAt(0));
        for(int i = 1; i < s.length(); i ++){
            if(!stack.isEmpty()){
            char tmp = stack.peek();
            if(tmp == s.charAt(i)){
                stack.pop();
            }
            else{
                stack.push(s.charAt(i));
            }
            }else{
                stack.push(s.charAt(i));
            }
        }
        StringBuilder sb = new StringBuilder();
        for(char c : stack){
            sb.append(c);
        }
        return sb.toString();
    }
}
```