# Search in Rotated Sorted Array
> Source: LintCode (https://www.lintcode.com/problem/62/)
## Problem Description
```
Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.
Example

Example 1:

Input:

array = [4, 5, 1, 2, 3]
target = 1

Output:

2

Explanation:

1 is indexed at 2 in the array.

Example 2:

Input:

array = [4, 5, 1, 2, 3]
target = 0

Output:

-1

Explanation:

0 is not in the array. Returns -1.
Challenge

O(logN) time
```

## C++ Solution
1. Binary Search method  
2. See code comments for detail  

Time Complexity: O(log(n)))  
Space Complexity: O(1)  
 
```
class Solution {
public:
    /**
     * @param A: an integer rotated sorted array
     * @param target: an integer to be searched
     * @return: an integer
     */
    int search(vector<int> &A, int target) {
        if (A.empty()) return -1;

        int left = 0;
        int right = A.size() - 1;
        
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            // now we have two cases: when comparing A[mid] to A[left]
            // case 1: mid and left are in same sorted ascending array, use binary search
            if (A[mid] >= A[left]) {
                if (target >= A[left] && target < A[mid]) {
                    right = mid;
                }
                else {
                    left = mid;
                }
            }
            // case 2: left is on the first ascending array, mid and right are in the second ascending array, still use binary search 
            else {
                if (target > A[mid] && target <= A[right]) {
                    left = mid;
                }
                else {
                    right = mid;
                }
            }
        }

        if (A[left] == target) return left;
        if (A[right] == target) return right;
        return -1;
    }
};
```
 