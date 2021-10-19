# Binary Tree Longest Consecutive Sequence
> Source: LintCode (https://www.lintcode.com/problem/595/)
## Problem Description
```
Given a binary tree, find the length of the longest consecutive sequence path.

The path refers to any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The longest consecutive path need to be from parent to child (cannot be the reverse).
Example

Example 1:

Input:

   1

    \

     3

    / \

   2   4

        \

         5

Output:3

Explanation:

Longest consecutive sequence path is 3-4-5, so return 3.

Example 2:

Input:

   2

    \

     3

    / 

   2    

  / 

 1

Output:2

Explanation:

Longest consecutive sequence path is 2-3,not 3-2-1, so return 2
```

 ### C++ Solution
 
 ```
/**
 * Definition of TreeNode:
 * class TreeNode {
 * public:
 *     int val;
 *     TreeNode *left, *right;
 *     TreeNode(int val) {
 *         this->val = val;
 *         this->left = this->right = NULL;
 *     }
 * }
 */

class Solution {
public:
    /**
     * @param root: the root of binary tree
     * @return: the length of the longest consecutive sequence path
     */
    int longestConsecutive(TreeNode * root) {
        if (root == nullptr) return 0;

        return dfs(root, nullptr, 0);
    }

    int dfs(TreeNode* node, TreeNode* parent, int lengthWithoutRoot) {
        if (node == nullptr) return 0;
        
        int length;
        if ((parent != nullptr) && (node->val == parent->val + 1)) {
            length = lengthWithoutRoot + 1;
        } 
        else {
            length = 1;
        }

        int leftLength = dfs(node->left, node, length);
        int rightLength = dfs(node->right, node, length);

        return max(max(leftLength, rightLength), length);
    }
};
 ```

 