# Minimum Depth of Binary Tree
> Source: LintCode (https://www.lintcode.com/problem/155/)
## Problem Description
```
Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.
Example

Example 1:

Input: {}

Output: 0

Example 2:

Input:  {1,#,2,3}

Output: 3	

Explanation:

	1

	 \ 

	  2

	 /

	3    

it will be serialized {1,#,2,3}

Example 3:

Input:  {1,2,3,#,#,4,5}

Output: 2	

Explanation: 

      1

     / \ 

    2   3

       / \

      4   5  

it will be serialized {1,2,3,#,#,4,5}
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
     * @param root: The root of binary tree
     * @return: An integer
     */
    int minDepth(TreeNode * root) {
        if (root == nullptr) return 0;
        return getMin(root);
    }

    int getMin(TreeNode* root) {
        if (root == nullptr) return INT_MAX;
        if (root->left == nullptr && root->right == nullptr) return 1;

        return min(getMin(root->left), getMin(root->right)) + 1;
    }
};
 ```

 