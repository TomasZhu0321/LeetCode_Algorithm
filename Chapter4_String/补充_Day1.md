# 925. Long Pressed Name
* **一刷:28:02(❌)**
* [925. Long Pressed Name](https://leetcode.com/problems/long-pressed-name/)

## Code
```java
class Solution {
    public boolean isLongPressedName(String name, String typed) {
        int i = 0, j = 0;
        int m = name.length(), n = typed.length();
        while (i< m && j < n) {
            if (name.charAt(i) == typed.charAt(j)) {  
                i++; j++;
            }
            else {
                if (j == 0) return false; 
                while (j < n-1 && typed.charAt(j) == typed.charAt(j-1)) j++;
                if (name.charAt(i) == typed.charAt(j)) { 
                    i++; j++;
                }
                else return false;
            }
        }
        if (i < m) return false;
        while (j < n) {
            if (typed.charAt(j) == typed.charAt(j-1)) j++;
            else return false;
        }
        return true;
    }
}
```
***
# 844. Backspace String Compar
* **一刷:28:02(❌)**
* [844. Backspace String Compar](https://leetcode.com/problems/backspace-string-compare/)
## My Code 
```java
class Solution {
    public boolean backspaceCompare(String s, String t) {
        Deque<Character> stack_s = new LinkedList<>();
        Deque<Character> stack_t = new LinkedList<>();
        int sIndex = 0;
        int tIndex = 0;
        while (sIndex < s.length()) {
            if (s.charAt(sIndex) != '#') {
                stack_s.push(s.charAt(sIndex));
            } else {
                if (!stack_s.isEmpty()) {
                    stack_s.pop();
                }
            }
            sIndex++;
        }
        while (tIndex < t.length()) {
            if (t.charAt(tIndex) != '#') {
                stack_t.push(t.charAt(tIndex));
            } else {
                if (!stack_t.isEmpty()) {
                    stack_t.pop();
                }
            }
            tIndex++;
        }
        if (stack_s.size() != stack_t.size())
            return false;
        while(!stack_s.isEmpty()){
            char a = stack_s.pop();
            char b = stack_t.pop();
            if (a != b) {
                return false;
            }
        }
        return true;
    }
}
```

* **双指针优化**:
  * **从后向前**遍历，遇到'#' 往前跳，当‘#’用完的时候比较大小
  * 具体操作:
    * 通过两个while循环模拟从后往前消除`#`.当没有`#`的时候，跳出while循环，进行比较
    * 当i或者j<0,就跳出整个循环
    * 如果他们不同时为-1，说明一方的字符串清理干净，另一边没有，`return false`
```java
class Solution {
    public boolean backspaceCompare(String s, String t) {
        int sSkipNum = 0; 
        int tSkipNum = 0; 
        char [] S = s.toCharArray();
        char [] T = t.toCharArray();
        int i = s.length() - 1;
        int j = t.length() - 1;
        while (true) {
            while (i >= 0) { 
                if (S[i] == '#') sSkipNum++;
                else {
                    if (sSkipNum > 0) sSkipNum--;
                    else break;
                }
                i--;
            }
            while (j >= 0) { 
                if (T[j] == '#') tSkipNum++;
                else {
                    if (tSkipNum > 0) tSkipNum--;
                    else break;
                }
                j--;
            }
            if (i < 0 || j < 0) break; 
            if (S[i] != T[j]) return false;
            i--;
            j--;
        }
        if (i == -1 && j == -1) return true;
        return false;
    }
}
```