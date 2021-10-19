# Unique Binary Search Trees
> Source: LintCode (https://www.lintcode.com/problem/163/)
## Problem Description
```
Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

Given n, how many structurally unique BSTs (binary search trees) that store values 1...n?
Example

Example 1:

Input:n = 3,

Output: 5

Explanation:there are a total of 5 unique BST's.

1           3    3       2      1

 \         /    /       / \      \

  3      2     1       1   3      2

 /      /       \                  \

2     1          2                  3

```

 ### C++ Solution
Use dynamic programming method. 
The base case that when n is 0 or 1, the answer is 1. So need to create an array of size at least 2 for base cases.

 
 ```
class Solution {
public:
    /**
     * @param n: An integer
     * @return: An integer
     */
    int numTrees(int n) {
        vector<int> dp(n + 2, 0);
        dp[0] = 1;
        dp[1] = 1;

        for (int i = 2; i <= n; i++) {
            for (int j = 0; j < i; j++) {
                dp[i] += dp[j] * dp[i - j - 1];
            }
        }

        return dp[n];
    }
};
 ```
 