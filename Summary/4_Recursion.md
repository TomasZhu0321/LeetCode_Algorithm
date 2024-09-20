# Things to Look Out for during Interview
* Define a **base case** so that recursion will end. 
* Clariy the **size of input data** : Beaware of cases where the recursion level goes too deep and causes a **stack overflow**
  * **Stack Overflow**: **Each recursive function call** allocates a new stack frame to store the function's **local variables, parameters and return address**. When the recursion depth becomes too large and exceeds the stack capacity, the system can no longer allocate stack frames, leading to a **stack overflow**.
  * 如何问？
    * To ensure that recursion is a feasible approach, could you let me know **the size of the input data**? I mean, large data sets could potentially cause a stack overflow due to **deep recursion**
  
# Corner Cases
* n == 0, n == 1
* base cases
* size of input data

# Techniques
## Memoization
* Memoization is suitable for **overlapping subproblems**. Specifically, Memoization avoids the repeated computation of the same subproblems during recursiong by storing their results in a cache. 
  
```java
public class FibonacciMemoization {
    private static HashMap<Integer, Integer> memo = new HashMap<>();

    public static int fibonacci(int n) {
        if (memo.containsKey(n)) {
            return memo.get(n);  // 如果 n 的结果已经计算过，直接返回
        }
        if (n <= 1) {
            return n;
        }
        // 递归计算并存储结果
        int result = fibonacci(n - 1) + fibonacci(n - 2);
        memo.put(n, result);  // 缓存计算结果

        return result;
    }
}
```
# LeetCode
## Essential questions
* [22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)
* [77. Combinations](https://leetcode.com/problems/combinations/)
* [78. Subsets](https://leetcode.com/problems/subsets/description/)

## Important
* [17. Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/)
* [90. Subsets II](https://leetcode.com/problems/subsets-ii/description/)
* [46. Permutations](https://leetcode.com/problems/permutations/description/)
* [37. Sudoku Solver](https://leetcode.com/problems/sudoku-solver/description/)
* [247. Strobogrammatic Number II](https://leetcode.com/problems/strobogrammatic-number-ii/description/)
  