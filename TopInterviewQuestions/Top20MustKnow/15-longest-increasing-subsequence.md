# Longest Increasing Subsequence
> Source: LintCode (https://www.lintcode.com/problem/76/)
## Problem Description
```
Given a sequence of integers, find the longest increasing subsequence (LIS).

You code should return the length of the LIS.

What's the definition of longest increasing subsequence?

    The longest increasing subsequence problem is to find a subsequence of a given sequence in which the subsequence's elements are in sorted order, lowest to highest, and in which the subsequence is as long as possible. This subsequence is not necessarily contiguous, or unique.

    https://en.wikipedia.org/wiki/Longest_increasing_subsequence

Example

Example 1:

Input:

nums = [5,4,1,2,3]

Output:

3

Explanation:

LIS is [1,2,3]
Example 2:

Input:

nums = [4,2,4,5,3,7]

Output:

4

Explanation:

LIS is [2,4,5,7]
Challenge

Time complexity O(n^2) or O(nlogn)
```

## C++ Solution 1
1. DP    
2. dp[i]: length of the LIS ends with nums[i]  
3. dp[] can init with 1 as each number has LIS 1  
4. transfer function: 
- loop through nums, can start at index 1  
- loop through nums before index i  
- only when the number before index i is smaller than nums[i], update dp  
- dp[i] = max(dp[i], dp[j] + 1)  


Time Complexity: O(n^2)   
Space Complexity: O(n)  
 
```
class Solution {
public:
    /**
     * @param nums: An integer array
     * @return: The length of LIS (longest increasing subsequence)
     */
    int longestIncreasingSubsequence(vector<int> &nums) {
        if (nums.empty()) return 0;
        int ans = 0;

        // dp: dp[i] = length of LTI that end with nums[i]
        // init dp to 1
        int n = nums.size();
        vector<int> dp(n, 1);

        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                // only update dp when the number before i is smaller
                if (nums[j] < nums[i]) {
                    // dp transfer fucntion: dp[i] is the max between dp[i] itself and the smaller number index j at dp[j]+1
                    dp[i] = max(dp[i], dp[j] + 1);
                }
            }
            // update the local return value for each index in nums
            ans = max(ans, dp[i]);
        }

        return ans;
    }
};
```
