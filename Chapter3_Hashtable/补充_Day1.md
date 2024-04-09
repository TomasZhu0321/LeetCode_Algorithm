# 205. Isomorphic Strings 
* **一刷:15:02(✅)**
* [205. Isomorphic Strings ](https://leetcode.com/problems/isomorphic-strings/)

## My Code
* 用Array表示ASCII码(128个): `boolean [] arr = new boolean [128]`
  * 然后直接用char引用: `arr[t.charAt(i)] = true;`
```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        Map<Character,Character> map = new HashMap<>();
        boolean [] arr = new boolean [128];
        for(int i = 0 ; i < s.length(); i ++){
            if( map.containsKey(s.charAt(i)) && map.get(s.charAt(i)) != t.charAt(i)){
                return false;
            }
            if(!map.containsKey(s.charAt(i))){
                if(arr[t.charAt(i)]){
                    return false;
                }
                map.put(s.charAt(i), t.charAt(i));
                arr[t.charAt(i)] = true;
            }
        }
        return true;
    }
}
```
***
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