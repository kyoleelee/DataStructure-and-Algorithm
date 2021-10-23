# Kth Largest Element
> Source: LintCode (https://www.lintcode.com/problem/5/)
## Problem Description
```
Find the K-th largest element in an array.

You can swap elements in the array.
1≤k≤1051 \leq k \leq 10^{5}1≤k≤105
Example

Example 1:

Input:

k = 1
nums = [1,3,4,2]

Output:

4

Explanation:

The first largest element is four.

Example 2:

Input:

k = 3
nums = [9,3,2,4,8]

Output:

4

Explanation:

The third largest largest element is four.
Challenge

O(n) time, O(1) extra memory.
```

## C++ Solution
1. Question ask for O(n), so cannot use sort  
2. Apply QuickSort method, when finding Kth element, it becomes a QuickSelect problem  
3. It is O(n) when using QuickSelect that sort the array  

Time Complexity: O(n)    
Space Complexity: O(1)  
 
```
class Solution {
public:
    /**
     * @param k: An integer
     * @param nums: An array
     * @return: the Kth largest element
     */
    int kthLargestElement(int k, vector<int> &nums) {
        int n = nums.size();
        if (n == 0 || k < 1 || k > n) return -1;

        // for coding purpose
        // transfer find kth largest to find (n - k)th smallest 
        return quickSelect(nums, n - k, 0, n - 1);
    }

    int quickSelect(vector<int>& nums, int k, int start, int end) {
        if (start >= end) return nums[k];

        int left = start, right = end;
        int pivot = nums[(start + end) / 2];

        while (left <= right) {
            while (left <= right && nums[left] < pivot) {
                left++;
            }
            while (left <= right && nums[right] > pivot) {
                right--;
            }
            if (left <= right) {
                swap(nums[left], nums[right]);
                left++;
                right--;
            }
        }

        if (k <= right) {
            return quickSelect(nums, k, start, right);
        }
        if (k >= left) {
            return quickSelect(nums, k, left, end);
        } 

        return nums[k];
    }
};
```
 