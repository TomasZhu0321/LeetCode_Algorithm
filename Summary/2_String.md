# String 底层
* In Java, String is internally stored as `Character Array`. The String class is immutable, meaning that once `String object` is created, its content cannot be changed.

# String 常用方法
* `length();`
  * TC: O(1) //不是O(n)
* `charAt(int index);` 
  * TC: O(1)
* `String newString = s.substring(start, end);` //end is not included
  * TC: O(m), where n is the length of substring, because substring will create a new String object
  * SC: O(m)
* `str1.equals(str2);` 
  * TC: O(n)
* `toUpperCase();` `toLowerCase()`
* `int result = str1.compareTo(str2);`
  * Def: Compare two strings lexicographically (dictionary order)
  * Return : `0` -- same, `- negative value` -- str1 is lexicographically less than the str2 ('apple' < 'bananda'; 'a' < 'ab') 
  * TC: O(n), where n is shorter string
* `String newStr = str.replace("Hello", "Hi");` //"Hello, Deming, Hello" --> "Hi, Deming Hi"
* `String newStr = str.replace('a', 'b');` 
  * TC:O(n)
* `boolean isSubstr = str.contains(substr);`
  * TC:O(m*n)
* `String [] strArr = str.split(',');`
  *  The argument provided to split() is treated as a regular expression. If you want to split by a special character (e.g., .), you need to escape it using double backslashes `\\. `
  *  Regular Expression: `+, -,*, ., ?, $`
*  `String res = String.join("", strArr);`和`String res = String.join("", strList);` 
    ```java
    List<String> list = Arrays.asList("apple", "banana", "orange");
    String result = String.join("", list);
    System.out.println(result);  // 输出: "applebananaorange"
    ```

# StringBuilder 常用方法
* `str.append("x");`
* `str.insert(index, "xx");` //insert at the index
* `str.delete(start,end);` // [start,end)
* `str.reverse();`
* `str.toString();`

# String 的转换
## String <=> StringBuilder
### String => StringBuilder
* Use `new StringBuilder(str);`
```java
String str1 = "abc";
StringBuilder sb = new StringBuilder(str1);
```
### StringBuilder => String
* Use `String str = sb.toString();`
## Integer <=> String || char <=> Integer || String <=> char
### Integer <=> String || char <=> Integer
* **Integer ==> String** : `String.valueOf(int a);`
* char ==> String: `String.valueOf(char a);`
```java
int a = 14;
String aStr = String.valueOf(a);
char b = 's';
String bStr= String.valueOf(b);
```
* **String ==> Integer**: `int a = Integer.parseInt(str);`
* String ==> char : `char b = str.charAt(0);`
* char <==> int: `int a = (int) b` //primitive type can transfer directly
## char [] charArr ==> String
* `String str = new String (charArr);`
  
## String [] strArr ==> String
* `String res = str.join("", strArr);`

# Corner Cases
* All English Letters? Lower Case or Upper Case?
* Specail characters?
* Empty String
* String with 1 or 2 characters
* String with repeated characters
* String with only distinct characters

# Techniques
## Counting Characters 
* Use **HashMap**. 
  * A common mistake is space complexity for **fixed constant** length is **O(1)**
## Anagram
* Rearranging the letters of a word to produce a new wrod, while using all the original letters only once
### Determine if two strings are anagrams
* Sorting both strings should produce the same resulting string
  * TC: O(N * log N) 
  * SC: O(logN)
  * Tips: Arrays.sort(charArr);
* Frequency counting of characters will help to determine if two strings are anagrams. (HashMap or similar)
  * TC: O(N)
  * SC: O(1)
## Palindrome
* Read the same backward as forward
### Determine Palindrome
* Hashtable is **NOT helpful !!!**
* **Reverse** the string and it should be equal to itself.
* Have **two pointers at the start and end** of the string. Move the pointers inward till they meet. At every point in time, the characters at both pointers should match
* When a problem is about **counting the number of palindromes**, a common trick is to have two pointers that move outward, away from middle. 
  * Note that palindromes can be even or odd length. For each middle pivot position, you need to check it **twice**
  * For **substrings**, we can terminate early once there is no match
  * For **subsequences**, use DP as there are overlapping subproblems

# LeetCode 
## Essential
* [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/)
* [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/description/)
* [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)

## Important
* [424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/description/)
* [438. Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/description/)
* [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/description/)
* * [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/description/)
* [5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/description/)
* [271. Encode and Decode Strings](https://leetcode.com/problems/encode-and-decode-strings/description/)