# Validate Binary Search Tree
> Source: LintCode (https://www.lintcode.com/problem/95/)
## Problem Description
```
Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

    The left subtree of a node contains only nodes with keys less than the node's key.
    The right subtree of a node contains only nodes with keys greater than the node's key.
    Both the left and right subtrees must also be binary search trees.
    A single node tree is a BST

Example

Example 1:

Input:

tree = {-1}

Output:

true

Explanation:

For the following binary tree（only one node）:
              -1
This is a binary search tree.

Example 2:

Input:

tree = {2,1,4,#,#,3,5}

Output:

true

Explanation:

For the following binary tree:
          2
         / \
        1   4
           / \
          3   5
This is a binary search tree.
```

## C++ Solution
1. Divide and Conquer  


Time Complexity: O(n)  
Space Complexity: O(1)  
 
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
     * @param root: The root of binary tree.
     * @return: True if the binary tree is BST, or false
     */
    bool isValidBST(TreeNode * root) {
        return helper(root, LLONG_MIN, LLONG_MAX);
    }

    bool helper(TreeNode* root, long min, long max) {
        if (root == nullptr) return true;
        if (root->val <= min || root->val >= max) {
            return false;
        }

        return helper(root->left, min, root->val) && helper(root->right, root->val, max);
    }
};
```
 