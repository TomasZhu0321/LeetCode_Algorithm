# 860. Lemonade Change
* **一刷:13:23(✅)**
* [860. Lemonade Change](https://leetcode.com/problems/lemonade-change/description/)

## My Code
```java
class Solution {
    public boolean lemonadeChange(int[] bills) {
        int fiveCharge = 0;
        int tenCharge = 0;
        for (int i = 0; i < bills.length; i++) {
            int cur = bills[i];
            if (cur == 5) {
                fiveCharge++;
            } else if (cur == 10) {
                if (fiveCharge <= 0)
                    return false;
                tenCharge++;
                fiveCharge--;
            } else {
                if (tenCharge > 0 && fiveCharge > 0) {
                    tenCharge--;
                    fiveCharge--;
                } else if (fiveCharge >= 3) {
                    fiveCharge = fiveCharge - 3;
                } else {
                    return false;
                }
            }
        }
        return true;
    }
}
```
