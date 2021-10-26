# Backpack
> Source: LintCode (https://www.lintcode.com/problem/92/)
## Problem Description
```
Given n items with size AiA_{i}Ai​ an integer m denotes the size of a backpack. How full you can fill this backpack?

You can not divide any item into small pieces.
Example

Example 1:

Input:

array = [3,4,8,5]
backpack size = 10

Output:

9

Explanation:

Load 4 and 5.

Example 2:

Input:

array = [2,3,5,7]
backpack size = 12

Output:

12

Explanation:

Load 5 and 7.
```

## C++ Solution
1. DP method  
2. dp[i][j] means for the first i items with first j size of bag, how much max can fill.  


Time Complexity: O(n*m)  
Space Complexity: O(n*m)  
 
```
class Solution {
public:
    /**
     * @param m: An integer m denotes the size of a backpack
     * @param A: Given n items with size A[i]
     * @return: The maximum size
     */
    int backPack(int m, vector<int> &A) {
        int n = A.size();
        
        vector<vector<int>> dp(n + 1, vector<int>(m + 1, 0));
        
        for (int i = 1; i <= n; i++) {
            for (int j = 0; j <= m; j++) {
                if (A[i - 1] > j) {
                    dp[i][j] = dp[i - 1][j];
                }
                else {
                    dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - A[i - 1]] + A[i - 1]);
                }
            }
        }
        
        return dp[n][m];
    }
};
```
 