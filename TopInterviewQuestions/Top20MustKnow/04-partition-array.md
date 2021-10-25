# Partition Array
> Source: LintCode (https://www.lintcode.com/problem/31/)
## Problem Description
```
Given an array nums of integers and an int k, partition the array (i.e move the elements in "nums") such that:

    All elements < k are moved to the left
    All elements >= k are moved to the right

Return the partitioning index, i.e the first index i nums[i] >= k.

You should do really partition in array nums instead of just counting the numbers of integers smaller than k.

If all elements in nums are smaller than k, then return nums.length
0 <= nums.length <= 20000
Example

Example 1:

Input:

nums = []
k = 9

Output:

0

Explanation:

Empty array, print 0.

Example 2:

Input:

nums = [3,2,2,1]
k = 2

Output:

1

Explanation:

the real array is[1,2,2,3].So return 1.
Challenge

Can you partition the array in-place and in O(n)?
```

## C++ Solution
1. Two pointer and pivot method  

Time Complexity: O(n)  
Space Complexity: O(1)  
 
```
class Solution {
public:
    /**
     * @param nums: The integer array you should partition
     * @param k: An integer
     * @return: The index after partition
     */
    int partitionArray(vector<int> &nums, int k) {
        if (nums.empty()) return 0;
        
        int left = 0; 
        int right = nums.size() - 1;
        while (left <= right) {
            while (left <= right && nums[left] < k) {
                left++;
            }
            
            while (left <= right && nums[right] >= k) {
                right--;
            }
            
            if (left <= right) {
                swap(nums[left], nums[right]);
                left++;
                right--;
            }
        }
        
        return left;
    }
};
```
 