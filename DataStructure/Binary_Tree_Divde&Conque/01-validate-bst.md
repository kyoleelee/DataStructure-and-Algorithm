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
        prev = nullptr;
        return inOrder(root);
    }

private:
    TreeNode* prev;
    bool inOrder(TreeNode* root) {
        if (root == nullptr) return true;
        if (!inOrder(root->left)) return false;
        if (prev && root->val <= prev->val) return false;
        prev = root; 
        return inOrder(root->right);
    }
};
```

 ### C++ Solution 1
This method is too straightforward like a brute force. 
Just convert the bst to an array, suppose a valid bst after inorder traversal shall become a sorted ascending array.
Loop throght the array, return false if find number is not in ascending, otherwise return true.
Two different coding are provided.
 
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
        if (root == nullptr) return true;
        vector<int> treeArray;
        inOrderTraversal(root, treeArray);
        return checkArraySorted(treeArray);
    }

    void inOrderTraversal(TreeNode* root, vector<int>& treeArray) {
        if (root == nullptr) return;
        inOrderTraversal(root->left, treeArray);
        treeArray.push_back(root->val);
        inOrderTraversal(root->right, treeArray);
    }

    bool checkArraySorted(vector<int> ary) {
        for (int i = 1; i < ary.size(); i++) {
            if (ary[i - 1] >= ary[i]) {
                return false;
            }
        }
        return true;
    }
};
 ```
 
  ### C++ Solution 2
This is divide and conque method. Given the boundary min, max of each subtree (left and right).
For left subtree, its max value shall be the root value.
For right subtree, its min value shall be the root value. 
 
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
 