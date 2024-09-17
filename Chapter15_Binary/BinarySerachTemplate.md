# Binary Search Template
* 左闭右闭
* 如果找第一个大于或等于 k的 return left
* 如果找第一个小于或等于 k的 return right

```java
public static int binarySearch(int[] arr, int target) {
    int l = 0;
    int r = arr.length - 1;
    // edge case
    if (arr[0] >= target) {
        return 0;
    }
    if (arr[arr.length - 1] < target) {
        return arr.length;
    }
    while (l <= r) {
        int mid = ((r - l) / 2) + l;
        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            l = mid + 1;
        } else {
            r = mid - 1;
        }
    }
    return l; //找的第一个大于或等于的
}
```