# 242. Valid Anagram
* **一刷:10:50(✅)**
* [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/description/)

## My Code
* 思路:通过HashMap,记录存入
  * .containsKey(`key`)
  * .remove(`key`)
  * .get(`key`)
  * .put(`key`,`value`)
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        int lenS = s.length();
        int lenT = t.length();
        if(lenS!=lenT) return false;
        HashMap<Character,Integer> hashMap = new HashMap<>();
        for(int i = 0; i < lenS; i ++){
            if(hashMap.containsKey(s.charAt(i))){
                int num = hashMap.get(s.charAt(i));
                num++;
                hashMap.put(s.charAt(i),num);
            }
            else {
                hashMap.put(s.charAt(i),1);
            }
        }
        for(int i = 0; i < lenT; i ++){
            if(hashMap.containsKey(t.charAt(i))){
                int num = hashMap.get(t.charAt(i));
                num --;
                if(num == 0){
                    hashMap.remove(t.charAt(i));
                }
                else{
                    hashMap.put(t.charAt(i),num);
                }
            }
            else{
                return false;
            }
        }
        if(hashMap.isEmpty()){
            return true;
        }
        return false;
    }
}
```

## Improvement
* 通过数组，`s.charAt(i) - 'a'` 来进行转换
```java
/**
 * 242. 有效的字母异位词 字典解法
 * 时间复杂度O(m+n) 空间复杂度O(1)
 */
class Solution {
    public boolean isAnagram(String s, String t) {
        int[] record = new int[26];

        for (int i = 0; i < s.length(); i++) {
            record[s.charAt(i) - 'a']++;     // 并不需要记住字符a的ASCII，只要求出一个相对数值就可以了
        }

        for (int i = 0; i < t.length(); i++) {
            record[t.charAt(i) - 'a']--;
        }
        
        for (int count: record) {
            if (count != 0) {               // record数组如果有的元素不为零0，说明字符串s和t 一定是谁多了字符或者谁少了字符。
                return false;
            }
        }
        return true;                        // record数组所有元素都为零0，说明字符串s和t是字母异位词
    }
}
```
