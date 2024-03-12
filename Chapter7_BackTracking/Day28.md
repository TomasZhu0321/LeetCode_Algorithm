# 93. Restore IP Addresses
* **一刷:30:22(✅)**
* [93. Restore IP Addresses](https://leetcode.com/problems/restore-ip-addresses/description/)

## My Code
* StringBuilder 的 `sb.delete(start,end);` 可以直接实现partition功能，并且在原字符串上修改
```java
class Solution {
    List<String> res = new LinkedList<>();
    int times = 0;

    public List<String> restoreIpAddresses(String s) {
        backTracking(s, 0);
        return res;
    }

    StringBuilder sb = new StringBuilder();

    private void backTracking(String s, int startIndex) {
        if (startIndex >= s.length() && times == 4) {
            sb.deleteCharAt(sb.length() - 1);
            res.add(sb.toString());
            return;
        }
        if (times > 4) {
            return;
        }
        for (int i = startIndex; i < s.length(); i++) {
            String tmp = s.substring(startIndex, i + 1);
            if (tmp.length() > 1 && tmp.charAt(0) == '0') {
                break;
            }
            if (tmp.length() > 3) {
                break;
            }
            int t = Integer.valueOf(tmp);
            if (t > 255) {
                break;
            }
            int prevLen = sb.length();
            sb.append(tmp).append('.');
            times++;
            backTracking(s, i + 1);
            times--;
            sb.delete(prevLen, sb.length());
        }
    }

}
```
***
# 78. Subsets
* **一刷:18:22(✅)**
* [78. Subsets](https://leetcode.com/problems/subsets/)

## My Code
```java
class Solution {
    List<List<Integer>> res = new LinkedList<>();
    List<Integer> tmp = new LinkedList<>();
    public List<List<Integer>> subsets(int[] nums) {
        backTracking(nums, 0);
        return res;
    }
    private void backTracking(int [] nums, int startIndex){
        if(startIndex <= nums.length){
            res.add(new LinkedList<>(tmp));
        }
        if(startIndex > nums.length){
            return;
        }
        for(int i = startIndex; i < nums.length; i ++){
            tmp.add(nums[i]);
            backTracking(nums, i + 1);
            tmp.removeLast();
        }
    }
}
```