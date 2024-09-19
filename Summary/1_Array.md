# Corner Cases
* Empty Sequence
* Sequence with 1 or 2 elements
* Duplicated elements in the sequence 
  * Need to clarify : 
  * - If there are duplicate values in the array? 
  * - Would the presence of duplicate values affect the answer?
  * - Does it make the question simpler or harder?

* **Slicing or Concatenating** arrays take O(n) time
* Use start and end indices to **demarcate** a subarray/range where possible.

# Techniques
## 🪐Sliding Window
* In a sliding window, the two pointers usually move in the same direction will never overtake each other.
### Situation
* These problems generally require **Finding Maximum/Minimum Subarray**, Substrings which satisfy some specific condition.
* The size of the subarray or substring ‘K’ will be given in some of the problems.
* Solving problems that require a fixed-size window to process elements

### Technique
#### 1. Fixed Size Sliding Window
1. Find the size of window required, say K
2. Compute the result for 1st window, (includ the first K elements)
3. Then use a loop to slide the window by 1 and keep computing the result window by window
#### 2. Variable Size Sliding Window
1. Increase our **right** pointer one by one till our condition is true
2. Shrink the size of our window by increasing **left** pointer
3. When condition is not satisfied, we start increasing the right pointer 
4. We iterate these steps until reach to the end

### TC : O(N)
### LeetCode
* [3.Longest SubString Without Repeating](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
* [209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)
* [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)

## 🪐Two Pointers
### Technique
#### 1. Slow and Fast Pointer 
* Move towards the same direction
#### 2. Start and End pointer
* One pointer (start) starts from the beginning while other pointer starts from the end

### TC : O(N)
### LeetCode
* [75. Sort Colors](https://leetcode.com/problems/sort-colors/)
* [647. Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/description/)

## 🪐Traversing From the Right
### LeetCode
* [739. Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)
* [1944. Number of Visible People in a Queue](https://leetcode.com/problems/number-of-visible-people-in-a-queue/)

## 🪐Sorting the Array (Binary Search)
### Situation
* Interviewer looking for solution faster than O(n) (Binary Search: O(log(N)))

### Binary Search 模版
* 左闭右闭
  * `left = mid + 1;`
  * `right = mid - 1;`
```java
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        if (nums[left] > target || nums[right] < target ) {
            return -1;
        }
        while (left <= right) {
            int mid = ((right - left) / 2 ) + left;
            if (nums[mid] == target) {
                return mid;
            }
            if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return -1;
    }
```

## 🪐Prefix Sum
### LeetCode
* [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)
* [209. Minimum size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)

## 🪐Index as a hash key
