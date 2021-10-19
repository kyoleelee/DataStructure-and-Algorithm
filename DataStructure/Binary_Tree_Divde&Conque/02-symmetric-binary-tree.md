# Symmetric Binary Tree
> Source: LintCode (https://www.lintcode.com/problem/46/)
## Problem Description
```
Given a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).
Example

Example 1:

Input: {1,2,2,3,4,4,3}

Output: true

Explanation:

         1

        / \

       2   2

      / \ / \

      3 4 4 3



is a symmetric binary tree.

Example 2:

Input: {1,2,2,#,3,#,3}

Output: false

Explanation:

         1

        / \

        2  2

        \   \

         3   3



is not a symmetric binary tree.

Challenge

Can you solve it both recursively and iteratively?
```

 ### C++ Solution 1
Recursive method
 
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
     * @param root: the root of binary tree.
     * @return: true if it is a mirror of itself, or false.
     */
    bool isSymmetric(TreeNode * root) {
        if (root == nullptr) return true;
        return helper(root->left, root->right);
    }

    bool helper(TreeNode* leftTree, TreeNode* rightTree) {
        if (leftTree == nullptr && rightTree == nullptr) return true;
        if ((leftTree != nullptr) && (rightTree != nullptr) && (leftTree->val == rightTree->val)) {
            return (helper(leftTree->right, rightTree->left) && helper(leftTree->left, rightTree->right));
        }
        return false;
    }
};
 ```

 