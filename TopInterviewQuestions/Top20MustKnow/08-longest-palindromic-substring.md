# Search in Rotated Sorted Array
> Source: LintCode (https://www.lintcode.com/problem/62/)
## Problem Description
```
Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.
Example

Example 1:

Input:"abcdzdcab"

Output:"cdzdc"

Example 2:

Input:"aba"

Output:"aba"

Challenge

O(n2) time is acceptable. Can you do it in O(n) time.
```

## C++ Solution 1
1. Two Pointer method  
2. The way to think a palindrome is that if a string is palindrome, then the string in the center should be also a palindrome  
   So it can starts from the middle to find the longest palindrome  
   let two pointers start from the middle, every time one pointer moves to left and the other one moves to right  
   if s[left] != s[right], the search for longest is over, use the left and right index to return the longest palindrome  
3. This problem we need consider two cases that the length of string can be either odd or even  
   When it's odd, the middle pointer are same for both left and right  
   When it's even, the middle pointer for left is mid and for right should be mid + 1  
4. Using two pointer method at this problem shall have time complexity of O(n^2) because the search of longest palindrome in one string is O(n)
   and the loop to pick up the center is also O(n) for entire string

Time Complexity: O(n^2)  
Space Complexity: O(1)  
 
```
class Solution {
public:
    /**
     * @param s: input string
     * @return: a string as the longest palindromic substring
     */
    string longestPalindrome(string &s) {
        // Two pointer method: O(n^2)
        if (s.size() < 2) return s;

        string ans = "";
        for (int i = 0; i < s.size(); ++i) {
            // case 1: if the string length is odd
            string odd = findLongestPalindrome(s, i, i);
            if (odd.size() > ans.size()) {
                ans = odd;
            }

            // case 2: if the string length is even
            string even = findLongestPalindrome(s, i, i + 1);
            if (even.size() > ans.size()) {
                ans = even;
            }
        }

        return ans;
    }

private:
    // this function is used to find the longest palindrome in a string
    // it starts from the middle of the string and two points moves to left and right 
    // becuase if the middler is palindrome, then check one to left and one to right that if the it is still palindrome
    string findLongestPalindrome(string str, int left, int right) {
        while (left >= 0 && right < str.size()) {
            if (str[left] != str[right]) {
                break;
            }
            left--;  // left pointer moves to left
            right++; // right pointer moves to right
        }
        return str.substr(left + 1, right - left - 1);
    }
};
```
 