# Sort Colors
> Source: LintCode (https://www.lintcode.com/problem/148/)
## Problem Description
```
Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

We will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

You are not suppose to use the library's sort function for this problem.
You should do it in-place (sort numbers in the original array).
You are not allowed to use counting sort to solve this problem.
Example

Example 1

Input : [1, 0, 1, 2]

Output : [0, 1, 1, 2]

Explanation : sort it in-place

Challenge

Could you come up with an one-pass algorithm using only O(1) space?
```

## C++ Solution  
1. Three Pointers  
2. Normal Two pointer (left, right) + one current pointer  
3. When current is 0 swap it to left, current and left increase  
4. When current is 2 swap it to right, only right decrease  
5. When current is 1, no swap just current increase  

Time Complexity: O(n)   
Space Complexity: O(1)  
 
```
class Solution {
public:
    /**
     * @param nums: A list of integer which is 0, 1 or 2 
     * @return: nothing
     */
    void sortColors(vector<int> &nums) {
        int n = nums.size();
        if (n == 0) return;
        
        int left = 0;
        int right = n - 1;
        int cur = 0;
        
        for (int i = 0; i < n; ++i) {
            if (nums[cur] == 0) {
                swap(nums[cur], nums[left]);
                cur++;
                left++;
            }
            else if (nums[cur] == 2) {
                swap(nums[cur], nums[right]);
                right--;
            }
            else {
                cur++;
            }
        }
    }
};
```
