# 125. Valid Palindrome
* **一刷:11：45(✅)**
* [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

## 字符常用方法
* `Character.isLetterOrDigit()`:判断是否是字母and数字
* `Character.toLowerCase()`:大写到小写

## Code
```java
class Solution {
    public boolean isPalindrome(String s) {
        int start = 0;
        int end = s.length() - 1;
        
        while (start < end) {
            // Move start to the next alphanumeric character
            while (start < end && !Character.isLetterOrDigit(s.charAt(start))) {
                start++;
            }
            // Move end to the previous alphanumeric character
            while (start < end && !Character.isLetterOrDigit(s.charAt(end))) {
                end--;
            }
            
            // Convert characters to lower case and compare
            if (Character.toLowerCase(s.charAt(start)) != Character.toLowerCase(s.charAt(end))) {
                return false;
            }
            
            start++;
            end--;
        }
        
        return true;
    }
}
```
## My Code
```java
class Solution {
    public boolean isPalindrome(String s) {
        char[] arr = s.toCharArray();
        int start = 0;
        int end = arr.length - 1;
        while (start < end) {
            // upper to lower
            if (arr[start] >= 'A' && arr[start] <= 'Z') {
                arr[start] = (char) (arr[start] + 32);
            }
            if (arr[end] >= 'A' && arr[end] <= 'Z') {
                arr[end] = (char) (arr[end] + 32);
            }
            // skip not belongs to alphanumeric
            while (!((arr[start] <= '9' && arr[start] >= '0') || (arr[start] >= 'a' && arr[start] <= 'z'))) {
                start++;
                if (start > end) {
                    return true;
                }
                if (arr[start] >= 'A' && arr[start] <= 'Z') {
                    arr[start] = (char) (arr[start] + 32);
                }
            }
            while (!((arr[end] <= '9' && arr[end] >= '0') || (arr[end] >= 'a' && arr[end] <= 'z'))) {
                end--;
                if (start > end) {
                    return true;
                }
                if (arr[end] >= 'A' && arr[end] <= 'Z') {
                    arr[end] = (char) (arr[end] + 32);
                }
            }
            if (arr[start] == arr[end]) {
                start++;
                end--;
            } else {
                return false;
            }
        }

        return true;
    }
}
```