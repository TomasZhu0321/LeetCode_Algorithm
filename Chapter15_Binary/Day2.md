# 528. Random Pick with Weight
* **一刷:20：45(❌)**
* [528. Random Pick with Weight](https://leetcode.com/problems/random-pick-with-weight/)

## 知识点
### 前缀和prefixSums
* 用处：可以快速计算出i在 它以及他之前的权重。**加权随机选择问题**中，前缀和数组有助于快速找到随机数落在哪个权重区间内.
* 结合**二分法**，能够实现按权重选取随机数

## Code
```java
class Solution {
    int [] preArr;
    int totalSum = 0;
    Random rand;
    public Solution(int[] w) {
        preArr = new int [w.length];
        int index = 0 ;
        for(int i : w){
            totalSum += i;
            preArr[index] = totalSum;
            index ++;
        }
        rand = new Random();
    }
    
    public int pickIndex() {
        int r = rand.nextInt(totalSum);
        int start = 0;
        int end = preArr.length - 1;
        while(start < end){
            int mid = start + (end - start)/2;
            if (preArr[mid] <= r){
                start = mid + 1;
            }
            else{
                end = mid;
            }
        }
        return end;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(w);
 * int param_1 = obj.pickIndex();
 */
```