# Convert Sorted Array to Binary Search Tree
> Source: LintCode(https://www.lintcode.com/problem/1359/?utm_source=%5B%27sc-github-wzz%27%5D)
## Problem Description
```
Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
Example

Example 1:

Input: [-10,-3,0,5,9]
Output: [0,-3,9,-10,#,5]
Explanation:
One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:
      0
     / \
   -3   9
   /   /
 -10  5
 
For this tree, you function need to return a tree node which value equals 0.

Example 2:

Input: [1,3]
Output: [3,1]
Explanation:
One possible answer is: [3,1], which represents the following height balanced BST:
  3
 / 
1   

For this tree, you function need to return a tree node which value equals 3.

```

 ### C++ Solution
 BST is a sorted array at in-order traversal, so the root of BST is the middle value of sorted array.
 The left sub tree is the left side before the middle of sorted array.
 The right sub tree is the right side after the middle of sorted array.
 
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
     * @param nums: the sorted array
     * @return: the root of the tree
     */
    TreeNode * convertSortedArraytoBinarySearchTree(vector<int> &nums) {
        if (nums.empty()) return nullptr;

        return buildTree(nums, 0, nums.size() - 1);
    }

    TreeNode* buildTree(vector<int> nums, int start, int end) {
        if (start > end) return nullptr;

        int mid = start + (end - start) / 2;
        TreeNode* tree = new TreeNode(nums[mid]);
        tree->left = buildTree(nums, start, mid - 1);
        tree->right = buildTree(nums, mid + 1, end);
        return tree;
    }
};
 ```
 