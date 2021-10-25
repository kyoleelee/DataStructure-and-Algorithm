# Longest Substring with At Most K Distinct Characters
> Source: LintCode (https://www.lintcode.com/problem/386/)
## Problem Description
```
Given a string S, find the length of the longest substring T that contains at most k distinct characters.
Example

Example 1:

Input: S = "eceba" and k = 3

Output: 4

Explanation: T = "eceb"

Example 2:

Input: S = "WORLD" and k = 4

Output: 4

Explanation: T = "WORL" or "ORLD"

Challenge

O(n) time
```

## C++ Solution
1. Two pointers on same direction  
2. Use Hash map to store the char and char count in the string  

Time Complexity: O(n)  
Space Complexity: O(n)  
 
```
class Solution {
public:
    /**
     * @param s: A string
     * @param k: An integer
     * @return: An integer
     */
    int lengthOfLongestSubstringKDistinct(string &s, int k) {
        int n = s.size();
        if (n == 0 || k == 0) return 0;
        
        unordered_map<char, int> charCount;
        int i = 0;
        int j = 0;
        int ans = 1;
        
        while (j < n) {
            charCount[s[j]]++;
            j++;
            
            // when there is no than k distinct char in hashmap
            // remove the most left char in current substring
            while (charCount.size() > k) {
                charCount[s[i]]--;
                // when there is multiple same char in the left 
                // move the left pointer and erase the last index char from hashmap
                if (charCount[s[i]] == 0) {
                    charCount.erase(s[i]);
                }
                i++;
            }
            
            ans = max(ans, j - i);
        }
        
        return ans;
    }
};
```
 