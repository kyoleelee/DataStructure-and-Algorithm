# Binary Tree Level Sum
> Source: LintCode(https://www.lintcode.com/problem/binary-tree-level-sum/?utm_source=sc-github-wzz)
## Problem Description
Given a binary tree and an integer which is the depth of the target level.

Calculate the sum of the nodes in the target level.
Example

Example 1:

Input：{1,2,3,4,5,6,7,#,#,8,#,#,#,#,9},2

Output：5 

Explanation：

     1

   /   \

  2     3

 / \   / \

4   5 6   7

   /       \

  8         9

2+3=5

Example 2:

Input：{1,2,3,4,5,6,7,#,#,8,#,#,#,#,9},3

Output：22

Explanation：

     1

   /   \

  2     3

 / \   / \

4   5 6   7

   /       \

  8         9

4+5+6+7=22
 

 ### C++ Solution
 
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
     * @param root: the root of the binary tree
     * @param level: the depth of the target level
     * @return: An integer
     */
    int levelSum(TreeNode * root, int level) {
        int sum = 0;
        dfs(root, sum, 1, level);
        return sum;
    }

    void dfs(TreeNode* node, int& sum, int depth, int level) {
        if (node == nullptr) return;
        if (depth == level) {
            sum += node->val;
        }
        dfs(node->left, sum, depth + 1, level);
        dfs(node->right, sum, depth + 1, level);
    }
};
 
 