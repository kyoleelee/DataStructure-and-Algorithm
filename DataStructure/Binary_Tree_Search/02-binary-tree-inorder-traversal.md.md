# Binary Tree Inorder Traversal
> Source: LintCode (https://www.lintcode.com/problem/67/)
## Problem Description
```
Given a binary tree, return the inorder traversal of its nodes‘ values.
Example

Example 1:

Input:

binary tree = {1,2,3}

Output:

[2,1,3]

Explanation:

   1
/  \
2     3
It will be serialized as {1,2,3} inorder traversal

Example 2:

Input:

binary tree = {1,#,2,3}

Output:

[1,3,2]

Explanation:

1
\
2
/
3
It will be serialized as {1,#,2,3} inorder traversal
Challenge

Can you do it without recursion?

```

 ### C++ Solution
Do it with iteration, because the recursion method is too straightforward. 
Use one stack for iteration method.
 
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
     * @param root: A Tree
     * @return: Inorder in ArrayList which contains node values.
     */
    vector<int> inorderTraversal(TreeNode * root) {
        vector<int> ans;
        stack<TreeNode*> stk;
        
        TreeNode* cur = root;
        while (cur != nullptr || !stk.empty()) {
            while (cur != nullptr) {
                stk.push(cur);
                cur = cur->left;
            }
            cur = stk.top();
            stk.pop();
            ans.push_back(cur->val);
            cur = cur->right;
        }

        return ans;
    }
};
 ```
 