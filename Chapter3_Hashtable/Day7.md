# 454. 4Sum II
* **一刷:15:32(✅)**
* [454. 4Sum II](https://leetcode.com/problems/4sum-ii/description/)

## My Code
```java
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        HashMap <Integer,Integer> map12 = new HashMap<>();
        for(int i = 0; i < nums1.length; i ++){
            for (int j = 0; j < nums2.length; j ++){
                int tmp = nums1[i] + nums2[j];
                if(map12.containsKey(tmp)){
                    int num = map12.get(tmp);
                    num ++;
                    map12.put(tmp,num);
                }
                else {
                    map12.put(tmp,1);
                }
            }
        }
        int res = 0;
        for(int i = 0; i < nums3.length; i ++){
            for (int j = 0; j < nums4.length; j ++){
                int tmp = -(nums3[i] + nums4[j]);
                if(map12.containsKey(tmp)){
                    res = res + map12.get(tmp);
                }
            }
        }
        return res;
    }
}
```