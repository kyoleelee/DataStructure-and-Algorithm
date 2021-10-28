# Word Ladder
> Source: LintCode (https://www.lintcode.com/problem/120/)
## Problem Description
```
Given two words (start and end), and a dictionary, find the shortest transformation sequence from start to end, output the length of the sequence.
Transformation rule such that:

    Only one letter can be changed at a time
    Each intermediate word must exist in the dictionary. (Start and end words do not need to appear in the dictionary )

    Return 0 if there is no such transformation sequence.
    All words have the same length.
    All words contain only lowercase alphabetic characters.
    You may assume no duplicates in the dictionary.
    You may assume beginWord and endWord are non-empty and are not the same.
    len(dict)<=5000,len(start)<5len(dict) <= 5000, len(start) < 5len(dict)<=5000,len(start)<5

Example

Example 1:

Input:

start = "a"
end = "c"
dict =["a","b","c"]

Output:

2

Explanation:

"a"->"c"

Example 2:

Input:

start ="hit"
end = "cog"
dict =["hot","dot","dog","lot","log"]

Output:

5

Explanation:

"hit"->"hot"->"dot"->"dog"->"cog"
```

## C++ Solution
1. Use BFS method  
2. Can use bi-direction BFS to improve the performance   

Time Complexity: O(26nL^2)   
Space Complexity: O(nL)  
26 means 26 chars, L is the word length      
 
```
class Solution {
public:
    /*
     * @param start: a string
     * @param end: a string
     * @param dict: a set of string
     * @return: An integer
     */
    int ladderLength(string &start, string &end, unordered_set<string> &dict) {
        if (dict.size() == 0) return 0;
        if (start == end) return 1;
        
        unordered_set<string> set;
        queue<string> q;
        q.push(start);
        set.insert(start);
        dict.insert(end);
        
        int ans = 1;
        while (!q.empty()) {
            ans++;
            int size = q.size();
            while (size--) {
                string word = q.front();
                q.pop();
                vector<string> next_words = nextWords(word, dict);
                for (auto next : next_words) {
                    if (next == end) return ans;
                    
                    if (!set.count(next)) {
                        q.push(next);
                        set.insert(next);
                    }
                }
            }
        }
        
        return 0;
    }
    
    // a help function to replace the given index in a word with given char
    string replaceWord(string word, int index, char c) {
        string tmp = word;
        tmp[index] = c;
        return tmp;
    }
    
    // given the word, loop through its each char and replace its char with 'a' to 'z'
    // after the replacement check if the new word is in dict and add it to return array if exist
    vector<string> nextWords(string word, unordered_set<string>& dict) {
        vector<string> ret;
        for (char i = 'a'; i <= 'z'; i++) {
            for (int j = 0; j < word.size(); j++) {
                // current char in word is equal to the replace char, skip to next replace char
                if (word[j] == i) {
                    continue;
                }
                // call the replace function to generate the new word with the char replaced
                string new_word = replaceWord(word, j, i);

                // new word is in dict, add new word to the return array
                if (dict.count(new_word)) {
                    ret.push_back(new_word);
                }
            }
        }
        return ret;
    }
};
```
 