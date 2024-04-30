# Quick Sort + Merge Sort + Quick Select
* 十大排序: [十大排序JavaGuide](https://javaguide.cn/cs-basics/algorithms/10-classical-sorting-algorithms.html#%E4%BB%A3%E7%A0%81%E5%AE%9E%E7%8E%B0-5)
## Quick Sort
* [java实现quick Sort](https://segmentfault.com/a/1190000040022056)
* [英文解释，很详细](https://www.geeksforgeeks.org/quick-sort/)
### 思想
* 方法：使用的**Divide and Conquer**
* Key Process: **partition()**
  * The target of partitions is to place the **pivot** at its correct position in the sorted array and put all **smaller** elements to the left of the pivot, and all **greater** elements to the right. 
  * Partiton is done **recursively** on each side of the pivot after the pivot is placed in its correct position and this finally sorts the array.
* ![image](./img/quicksort_1.png)
* **代码逻辑**
  * 1. Set the `pivot = arr[high];`
  * 2. Start from the **leftmost** which is `i = low`. And keep track of the index of **smaller elements** as `int pointer`
  * 3. if current value `arr[i]` smaller than pivot, than **swap** the `arr[pointer]` with `arr[i]`  
  * 4. After the traversing, swap the pointer and pivot, and go on
![image](./img/quicksort_2.png)
![image](./img/quicksort_3.png)
### Time Complexity and Auxiliary Space
#### Time Complexity
* Best Case: $\omega$ (NlogN)
  * When the pivot chosen at the each step divides the array into roughly **equal halves**
    * Which mean at **each step of recursion**, the time complexity is $O(n)$
    * The **depth** of recursion is roughly $O(logN)$
    *  ==> $\omega$ (N * logN)
* Worst Case: $O(N * N)$
  * When the pivot chosen at the each step results in **highly unbalanced paritions** (When the array is already sorted and the pivot is always chosen as the smallest or largest element.)
    * One arr is void, and the other one contains all the elements left
    * ==> $O(N * N)$
#### Auxiliary Space
* Depends on the depth of **recursion**
  * Best case: $\omega$ (logN)
  * Worst case: $O(N)$
### 代码实现
```java

public class QuickSort {

    public static int partition(int[] array, int low, int high) {
        // 取最后一个元素作为中心元素
        int pivot = array[high];
        // 定义指向比中心元素大的指针，首先指向第一个元素
        int pointer = low;
        // 遍历数组中的所有元素，将比中心元素大的放在右边，比中心元素小的放在左边
        for (int i = low; i < high; i++) {
            if (array[i] <= pivot) {
                // 将比中心元素小的元素和指针指向的元素交换位置
                // 如果第一个元素比中心元素小，这里就是自己和自己交换位置，指针和索引都向下一位移动
                // 如果元素比中心元素大，索引向下移动，指针指向这个较大的元素，直到找到比中心元素小的元素，并交换位置，指针向下移动
                int temp = array[i];
                array[i] = array[pointer];
                array[pointer] = temp;
                pointer++;
            }
            System.out.println(Arrays.toString(array));
        }
        // 将中心元素和指针指向的元素交换位置
        int temp = array[pointer ];
        array[pointer] = array[high];
        array[high] = temp;
        return pointer;
    }

    public static void quickSort(int[] array, int low, int high) {
        if (low < high) {
            // 获取划分子数组的位置
            int position = partition(array, low, high);
            // 左子数组递归调用
            quickSort(array, low, position -1);
            // 右子数组递归调用
            quickSort(array, position + 1, high);
        }
    }

    public static void main(String[] args) {
        int[] array = {6,72,113,11,23};
        quickSort(array, 0, array.length -1);
        System.out.println("排序后的结果");
        System.out.println(Arrays.toString(array));
    }
}
```