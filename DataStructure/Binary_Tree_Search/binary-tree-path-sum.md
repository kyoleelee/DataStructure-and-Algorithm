# Binary Tree Path Sum
> Source: LintCode(https://www.lintcode.com/problem/376/?utm_source=%5B%27sc-github-wzz%27%5D)
## Problem Description
```
Given a binary tree, find all paths that sum of the nodes in the path equals to a given number target.

A valid path is from root node to any of the leaf nodes.
Example

Example 1:

Input:

{1,2,4,2,3}

5

Output: [[1, 2, 2],[1, 4]]

Explanation:

The tree is look like this:

	     1

	    / \

	   2   4

	  / \

	 2   3

For sum = 5 , it is obviously 1 + 2 + 2 = 1 + 4 = 5

Example 2:

Input:

{1,2,4,2,3}

3

Output: []

Explanation:

The tree is look like this:

	     1

	    / \

	   2   4

	  / \

	 2   3

Notice we need to find all paths from root node to leaf nodes.

1 + 2 + 2 = 5, 1 + 2 + 3 = 6, 1 + 4 = 5 

There is no one satisfying it.
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
    /*
     * @param root: the root of binary tree
     * @param target: An integer
     * @return: all valid paths
     */
    vector<vector<int>> binaryTreePathSum(TreeNode * root, int target) {
        vector<int> path;
        vector<vector<int>> ans;
        int sum = 0;
        dfs(root, target, sum, path, ans);
        return ans;
    }

    void dfs(TreeNode* node, int target, int& sum, vector<int>& path, vector<vector<int>>& ans) {
        if (node == nullptr) return;
        
        path.push_back(node->val);
        sum += node->val;
        if (node->left == nullptr && node->right == nullptr && sum == target) {
            ans.push_back(path);
        }

        dfs(node->left, target, sum, path, ans);
        dfs(node->right, target, sum, path, ans);

        sum -= path.back();
        path.pop_back();
    }
};
 ```
 