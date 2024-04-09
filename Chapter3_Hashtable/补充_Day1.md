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
