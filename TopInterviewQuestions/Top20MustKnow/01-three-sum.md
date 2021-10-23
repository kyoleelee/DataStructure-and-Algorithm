# 3Sum
> Source: LintCode (https://www.lintcode.com/problem/57/)
## Problem Description
```
Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Elements in a triplet (a,b,c) must be in non-descending order. (ie, a ≤ b ≤ c)

The solution set must not contain duplicate triplets.
Example

Example 1:

Input:

numbers = [2,7,11,15]

Output:

[]

Explanation:

Cannot find triples such that the sum of three numbers is 0.
Example 2:

Input:

numbers = [-1,0,1,2,-1,-4]

Output:

[[-1, 0, 1],[-1, -1, 2]]

Explanation:

[-1, 0, 1] and [-1, -1, 2] are two triples.1, 2]]
```

## C++ Solution
1. Sort the array first 
2. locate the first number in array and use two pointer method at the rest of array 

Time Complexity: O(n^2)  
Space Complexity: O(n)  
 
 ```
class Solution {
public:
    /**
     * @param numbers: Give an array numbers of n integer
     * @return: Find all unique triplets in the array which gives the sum of zero.
     */
    vector<vector<int>> threeSum(vector<int> &numbers) {
        vector<vector<int>> ans;
        sort(numbers.begin(), numbers.end());
        int n = numbers.size();
        if (n < 3 || numbers[0] > 0) return ans;

        for (int i = 0; i < n - 2; ++i) {
            // skip the duplicate number at i
            if (i > 0 && numbers[i] == numbers[i - 1]) {
                continue;
            }

            int target = 0 - numbers[i];
            int j = i + 1; 
            int k = n - 1;
            while (j < k) {
                if (numbers[j] + numbers[k] < target) {
                    ++j;
                }
                else if (numbers[j] + numbers[k] > target) {
                    --k;
                }
                else {
                    ans.push_back({numbers[i], numbers[j], numbers[k]});
                    ++j;
                    --k;
                    // skip duplicate number at j and k
                    while (j < k && numbers[j] == numbers[j - 1]) {
                        ++j;
                    }
                    while (j < k && numbers[k] == numbers[k + 1]) {
                        --k;
                    }
                }
            }
        }

        return ans;
    }
};
 ```
 