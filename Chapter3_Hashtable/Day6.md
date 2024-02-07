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
***
# 1002. Find Common Characters
* **一刷:25:50(✅)**
* [1002. Find Common Characters](https://leetcode.com/problems/find-common-characters/description/)

## My Code
```java
class Solution {
    public List<String> commonChars(String[] words) {
        int [] arr = new int [26];
        int len = words.length;
        List<String> res = new ArrayList<>();
        for(int i = 0; i < words[0].length(); i ++){
            int index = words[0].charAt(i) - 'a';
            arr[index] ++;
        }
        for(int i = 1; i < words.length; i ++){
            int [] tmp = new int [26];
            for(int j = 0; j < words[i].length(); j ++){
                int index = words[i].charAt(j) - 'a';
                tmp[index] ++;
            }
            for(int z = 0; z < 26; z ++){
                arr[z] = Math.min(arr[z],tmp[z]);
            }
        }
        for(int i = 0; i < 26; i ++){
            int times = arr[i];
            if(times > 0){
            for(int j = 0; j < times; j ++){
                res.add(String.valueOf((char)(i + 'a')));
                }
            }
        }
        return res;
    }
}
```
***
# 349. Intersection of Two Arrays
* **一刷:10:42(✅)**
* [349. Intersection of Two Arrays](https://leetcode.com/problems/intersection-of-two-arrays/)

## My Code
```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        HashSet <Integer> hashSet = new HashSet<>();
        for(int i:nums1){
            hashSet.add(i);
        }
        HashSet<Integer> res = new HashSet<>();
        for(int i : nums2){
            if(hashSet.contains(i)){
                res.add(i);
            }
        }
        int [] arr = new int[res.size()];
        int j = 0;
        for(int i : res){
            arr[j] = i;
            j ++;
        }
        return arr;
    }
}
```
***
# 202. Happy Number
* **一刷:30:50(✅)**
* [202. Happy Number](https://leetcode.com/problems/happy-number/description/)

## My Code
```java
class Solution {
    public boolean isHappy(int n) {
        HashSet<Integer> res = new HashSet<>();
        res.add(n);
        while(n != 1 ){
            int tmp = 0;
            while(n > 0){
                tmp += (n%10)*(n%10);
                n = n/10;
            }
            if(res.contains(tmp)){
                return false;
            }
            else{
                res.add(tmp);
            }
            n = tmp;
        }
        return true;
    }
}
***

