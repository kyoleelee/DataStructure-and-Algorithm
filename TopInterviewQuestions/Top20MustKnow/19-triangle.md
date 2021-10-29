# Triangle
> Source: LintCode (https://www.lintcode.com/problem/109/)
## Problem Description
```
Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

Bonus point if you are able to do this using only O(n)O(n)O(n) extra space, where n is the total number of rows in the triangle.
Example

Example 1:

Input:

triangle = [
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]

Output:

11

Explanation:

The minimum path sum from top to bottom is 11 (2 + 3 + 5 + 1 = 11).

Example 2:

Input:

triangle = [
     [2],
    [3,2],
   [6,5,7],
  [4,4,8,1]
]

Output:

12

Explanation:

The minimum path sum from top to bottom is 12 (2 + 2 + 7 + 1 = 12).
```

## C++ Solution 1
1. DP with two dimensional array  
2. The 2D array, row is the number of rows triangle, and column should be number of elements of last row of triangle  

Time Complexity: O(n^2)
Space Complexity: O(n^2)  
 
```
class Solution {
public:
    /**
     * @param triangle: a list of lists of integers
     * @return: An integer, minimum path sum
     */
    int minimumTotal(vector<vector<int>> &triangle) {
        int n = triangle.size();
        int m = triangle.back().size(); // last line size of triangle
        if (n == 0 || m == 0)
            return 0;
        
        vector<vector<int>> dp(n, vector<int>(m, INT_MAX));
        for (int i = 0; i < m; i++) {
            // init the last row of dp with the last row value from triangle
            dp[n - 1][i] = triangle[n - 1][i];
        }
        
        // from bottom to top dp[i][j] is the min between dp[i+1][j] and dp[i+1][j+1]
        for (int i = n - 2; i >= 0; i--) {
            for (int j = 0; j < triangle[i].size(); j++) {
                dp[i][j] = min(dp[i + 1][j], dp[i + 1][j + 1]) + triangle[i][j];
            }
        }
        
        // this is bottom to top DP method, so [0][0] is the final answer for min path from top to bottom
        return dp[0][0];
    }
};
```

## C++ Solution 2
1. DP with two dimensional array, we use roller array skill to optimize the space complexity  
2. We only need two row in the 2D array, not n rows of number of triangle rows  
3. The coding is almost same, except use mod 2 at place where updates dp[i] 

Time Complexity: O(n^2)
Space Complexity: O(n)  
 
```
class Solution {
public:
    /**
     * @param triangle: a list of lists of integers
     * @return: An integer, minimum path sum
     */
    int minimumTotal(vector<vector<int>> &triangle) {
        int n = triangle.size();
        int m = triangle.back().size(); // last line size of triangle
        if (n == 0 || m == 0)
            return 0;
        
        // using roller array to optimize space complexity from O(n^2) to O(n)
        // only needs 2 row here
        vector<vector<int>> dp(2, vector<int>(m, INT_MAX));
        for (int i = 0; i < m; i++) {
            // init the last row of dp with the last row value from triangle
            dp[(n - 1) % 2][i] = triangle[n - 1][i];
        }
        
        // from bottom to top dp[i][j] is the min between dp[i+1][j] and dp[i+1][j+1]
        for (int i = n - 2; i >= 0; i--) {
            for (int j = 0; j < triangle[i].size(); j++) {
                dp[i % 2][j] = min(dp[(i + 1) % 2][j], dp[(i + 1) % 2][j + 1]) + triangle[i][j];
            }
        }
        
        // this is bottom to top DP method, so [0][0] is the final answer for min path from top to bottom
        return dp[0][0];
    }
};
```