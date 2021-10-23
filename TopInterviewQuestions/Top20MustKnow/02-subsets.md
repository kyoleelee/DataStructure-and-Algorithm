# Subsets
> Source: LintCode (https://www.lintcode.com/problem/17/)
## Problem Description
```
Given a set with distinct integers, return all possible subsets.

    Elements in a subset must be in non-descending order.
    The solution set must not contain duplicate subsets.

Example

Example 1:

Input:

nums = [0] 

Output:

[ 
  [], 
  [0] 
] 

Explanation:

The subsets of [0] are only [] and [0].

Example 2:

Input:

nums = [1,2,3] 

Output:

[ 
  [3], 
  [1], 
  [2], 
  [1,2,3], 
  [1,3], 
  [2,3], 
  [1,2], 
  [] 
] 

Explanation:

The subsets of [1,2,3] are [], [1], [2], [3], [1,2], [1,3], [2,3], [1,2,3].
Challenge

Can you do it in both recursively and non-recursively?
```

## C++ Solution 1
1. Recursive
2. Apply DFS algorithm for recursive  
3. 'Subsets' is a combination problem to find all possible combination, so it will take 2^n * n   

Time Complexity: O(2^n * n)  
Space Complexity: O(2^n * n)  
 
```
class Solution {
public:
    /**
     * @param nums: A set of numbers
     * @return: A list of lists
     */
    vector<vector<int>> subsets(vector<int> &nums) {
        vector<int> subset;
        vector<vector<int>> subsets;

        sort(nums.begin(), nums.end());
        dfs(nums, 0, subset, subsets);

        return subsets;
    }

    void dfs(vector<int>& nums, int start, vector<int>& subset, vector<vector<int>>& subsets) {
        subsets.push_back(subset);

        for (int i = start; i < nums.size(); i++) {
            subset.push_back(nums[i]);
            dfs(nums, i + 1, subset, subsets);
            subset.pop_back();
        }
    }
};
```

## C++ Solution 2
1. Iterative
2. Apply BFS algorithm for non-recursive  
3. 'Subsets' is a combination problem to find all possible combination, so it will take 2^n * n   

Time Complexity: O(2^n * n)  
Space Complexity: O(2^n * n)  
 
```
class Solution {
public:
    /**
     * @param nums: A set of numbers
     * @return: A list of lists
     */
    vector<vector<int>> subsets(vector<int> &nums) {
        vector<vector<int>> ans;
        sort(nums.begin(), nums.end());

        queue<vector<int>> q;
        q.push({});
        while (!q.empty()) {
            auto subset = q.front();
            q.pop();
            ans.push_back(subset);

            for (int num : nums) {
                if (subset.empty() || subset.back() < num) {
                    auto new_subset = subset;
                    new_subset.push_back(num);
                    q.push(new_subset);
                }
            }
        }
        
        return ans;
    }
};
```
 
## C++ Solution 3
1. Iterative
2. Apply Bit Manipulate for non-recursive  
3. 'Subsets' is a combination problem to find all possible combination, so it will take 2^n * n   

Time Complexity: O(2^n * n)  
Space Complexity: O(2^n * n)  
 
```
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> ans;
        int n = nums.size();
        
        // 2^n = 1<<n 
		// there is 2^n combination when thinking as binary representation
        for (int i = 0; i < (1 << n); i++) {
            vector<int> subset;
            for (int j = 0; j < n; j++) {
                // convert i to binary and check if there is a bit is 1
                if ((i >> j) & 1 != 0) {
                    subset.push_back(nums[j]);
                }
            }
            ans.push_back(subset);
        }
        return ans;
    }
};
```