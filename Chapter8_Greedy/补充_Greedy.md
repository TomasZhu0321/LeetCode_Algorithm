# 649. Dota2 Senate
* **一刷:37:49(❌)**
* [649. Dota2 Senate](https://leetcode.com/problems/dota2-senate/)

## 思路
* while循环 ==> 当双方R/D有一方被完全消灭了，游戏结束
![image](./img/649.jpeg)
![image](./img/649_1.jpg)

```java
class Solution {
    public String predictPartyVictory(String senate) {
        char[] senates = senate.toCharArray();
        boolean R = true;
        boolean D = true;
        int flag = 0;
        while (R && D) {
            R = false;
            D = false;
            for (int i = 0; i < senates.length; i++) {
                if (senates[i] == 'R') {
                    if (flag < 0) {
                        senates[i] = '0';
                    } else {
                        R = true;
                    }
                    flag++;
                }
                if (senates[i] == 'D') {
                    if (flag > 0) {
                        senates[i] = '0';
                    } else {
                        D = true;
                    }
                    flag--;
                }
            }
        }
        return R == true ? "Radiant" : "Dire";
    }
}
```