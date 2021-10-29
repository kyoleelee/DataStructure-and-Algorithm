# Jump Game
> Source: LintCode (https://www.lintcode.com/problem/116/)
## Problem Description
```
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

The array A contains 𝑛 integers 𝑎1, 𝑎2, …, 𝑎𝑛 (1≤𝑎𝑖≤5000) (1≤n≤5000 )
Example

Example 1:

Input:

A = [2,3,1,1,4]

Output:

true

Explanation:

0 -> 1 -> 4 (the number here is subscript) is a reasonable scheme.

Example 2:

Input:

A = [3,2,1,0,4]

Output:

false

Explanation:

There is no solution that can reach the end.
Challenge

This problem have two method which is Greedy and Dynamic Programming.

The time complexity of Greedy method is O(n)O(n)O(n).

The time complexity of Dynamic Programming method is O(n2)O(n^2)O(n2).

We manually set the small data set to allow you pass the test in both ways. This is just to let you learn how to use this problem in dynamic programming ways. If you finish it in dynamic programming ways, you can try greedy method to make it accept again.
```

## C++ Solution 1
1. DP  
2. dp[i] means if it is possible to jump to index i  
3. dp[0] can init to TRUE becuase we are given to start at index 0  
4. the rest dp is init to FLASE and we start from index 1 to loop  
5. transfer function: if exist j that dp[j] is TRUE and it can jump from j to i, we set dp[i] to TRUE
   otherwise dp[i] is FALSE  

Time Complexity: O(n^2)  
Space Complexity: O(n)  
 
```
class Solution {
public:
    /**
     * @param A: A list of integers
     * @return: A boolean
     */
    bool canJump(vector<int> &A) {
        int n = A.size();
        if (n == 0) return false;
        
        // dp[i] means if it is possible to jump to index i
        // init dp[0] to true and rest to false
        vector<bool> dp(n, false);
        dp[0] = true;
        
        for (int i = 1; i < n; i++) {
            // the dp transfer function:
            // dp[i] is true when there is a index j before i
            // that dp[j] is true and it can jump from j to i 
            for (int j = 0; j < i; j++) {
                if ((dp[j] == true) && (j + A[j] >= i)) {
                    dp[i] = true;
                    break;
                }
            }
        }
        
        return dp[n-1];
    }
};
```

## C++ Solution 2
1. Greedy Algorithm  
2. Maintain a right most reachable index (rightMost) in real time  
3. Loop through array with index i, if i is less than rightMost, update rightMost with max(rightMost, i+A[i])  
4. If rightMost is >= the last index return TRUE, otherwise return FALSE after the loop is over  

Time Complexity: O(n)  
Space Complexity: O(1)  
 
```
class Solution {
public:
    /**
     * @param A: A list of integers
     * @return: A boolean
     */
    bool canJump(vector<int> &A) {
        int n = A.size();
        int rightmost = 0;
        for (int i = 0; i < n; ++i) {
            if (i <= rightmost) {
                rightmost = max(rightmost, i + A[i]);
                if (rightmost >= n - 1) {
                    return true;
                }
            }
        }
        return false;
    }
};
```