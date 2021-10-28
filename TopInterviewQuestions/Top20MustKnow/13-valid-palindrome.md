# Valid Palidrome
> Source: LintCode (https://www.lintcode.com/problem/415/)
## Problem Description
```
Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.
Example

Example 1:

Input: "A man, a plan, a canal: Panama"

Output: true

Explanation: "amanaplanacanalpanama"

Example 2:

Input: "race a car"

Output: false

Explanation: "raceacar"

Challenge

O(n) time without extra memory.
```

## C++ Solution
1. Two pointer  


Time Complexity: O(n)  
Space Complexity: O(1)  
 
```
class Solution {
public:
    /**
     * @param s: A string
     * @return: Whether the string is a valid palindrome
     */
    bool isPalindrome(string &s) {
        if (s.empty()) return true;
        
        int left = 0;
        int right = s.size() - 1;
        
        while (left < right) {
            while (left < right && !isalpha(s[left]) && !isdigit(s[left])) {
                left++;
            }
            
            while (left < right && !isalpha(s[right]) && !isdigit(s[right])) {
                right--;
            }
            
            if (tolower(s[left]) != tolower(s[right])) {
                return false;
            }
            
            left++;
            right--;
        }
        
        return true;
    }
};
```
 