# Wood Cut
> Source: LintCode (https://www.lintcode.com/problem/183/)
## Problem Description
```
Given n pieces of wood with length L[i] (integer array). Cut them into small pieces to guarantee you could have equal or more than k pieces with the same length. What is the longest length you can get from the n pieces of wood? Given L & k, return the maximum length of the small pieces.

The unit of length is centimeter.The length of the woods are all positive integers,you couldn't cut wood into float length.If you couldn't get >= k pieces, return 0.
Example

Example 1

Input:

L = [232, 124, 456]

k = 7

Output: 114

Explanation: We can cut it into 7 pieces if any piece is 114cm long, however we can't cut it into 7 pieces if any piece is 115cm long.

Example 2

Input:

L = [1, 2, 3]

k = 7

Output: 0

Explanation: It is obvious we can't make it.

Challenge

O(n log Len), where Len is the longest length of the wood.
```

## C++ Solution
1. Binary Search Method and it searches at answers.  
2. It still uses normal binary search template, only change the condition comparison part  
3. The question is looking for length, we know the possible length is between 1 to max length.  
   So we can perform binary search in range of possible lengths.  
   Pick up a middle length first, if it can cut with middle, we go to search between middle and max.  
   Otherwise we search between 1 to middler. 

Time Complexity: O(nlog(n)) = O(nlog(L)) here  
Space Complexity: O(1)  
 
```
class Solution {
public:
    /**
     * @param L: Given n pieces of wood with length L[i]
     * @param k: An integer
     * @return: The maximum length of the small pieces
     */
    int woodCut(vector<int> &L, int k) {
        if (L.empty()) return 0;

        sort(L.begin(), L.end());
        int left  = 1;
        int right = L.back();

        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (isCutable(L, k, mid)) {
                left = mid;
            }
            else {
                right = mid;
            }
        }

        if (isCutable(L, k, right)) 
            return right;

        if (isCutable(L, k, left))
            return left;

        return 0;
    }

    bool isCutable(vector<int>& L, int k, int piece) {
        int n = 0;
        for (auto l : L) {
            n += l / piece;
        }
        return n >= k ? true : false;
    }
};
```
 