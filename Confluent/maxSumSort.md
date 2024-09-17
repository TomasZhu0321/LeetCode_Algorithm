# 问题
```Given two arrays where array a is fixed and array b can be rearranged, the objective is to rearrange array b in such a way that as many numbers in b as possible are greater than their corresponding numbers in a. Finally, calculate the sum of the numbers in b that are greater than the corresponding numbers in a. For example, if a = [1, 2, 3, 4, 5] and b = [2, 6, 4, 3, 5], return 2 + 3 + 4 + 5 + 6 = 20.
```
```
Example
Input:
a = [1, 2, 3, 4, 5]
b = [2, 6, 4, 3, 5]
Output:
20
Constraints
Arrays a and b have the same length.
Both arrays contain positive integers.
```
## Code

```java
package org.example;

import java.util.Arrays;

class MaxSumOfB {

    public static int maxSum(int[] a, int[] b) {
        // 排序数组 a 和 b
        Arrays.sort(a);
        Arrays.sort(b);

        int n = a.length;
        int sum = 0;
        int j = 0;

        // 遍历数组 a 和 b
        for (int i = 0; i < n; i++) {
            // 找到 b 中大于 a 的对应元素
            while (j < n && b[j] <= a[i]) {
                j++;
            }
            // 如果找到了，累加到结果中并移动指针
            if (j < n) {
                sum += b[j];
                j++;
            }
        }

        return sum;
    }

    public static void main(String[] args) {
        int[] a1 = {1, 2, 3, 4, 5};
        int[] b1 = {2, 6, 4, 3, 5};
        System.out.println(maxSum(a1, b1)); // 输出: 20

        int[] a2 = {4, 1, 2};
        int[] b2 = {3, 6, 2};
        System.out.println(maxSum(a2, b2)); // 输出: 11
    }
}

```