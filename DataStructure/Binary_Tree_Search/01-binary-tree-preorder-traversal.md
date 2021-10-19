# Binary Tree Preorder Traversal
> Source: LintCode (https://www.lintcode.com/problem/66/)
## Problem Description
```
Given a binary tree, return the preorder traversal of its nodes' values.

    The first data is the root node, followed by the value of the left and right son nodes, and "#" indicates that there is no child node.
    The number of nodes does not exceed 20.

Example

Example 1:

Input:

binary tree = {1,2,3}

Output:

[1,2,3]

Explanation:

   1
/  \
2     3
It will be serialized as {1,2,3} preorder traversal

Example 2:

Input:

binary tree = {1,#,2,3}

Output:

[1,2,3]

Explanation:

1
\
2
/
3
It will be serialized as {1,#,2,3} preorder traversal
Challenge

Can you do it without recursion?

```

 ### C++ Solution
Do it with iteration, because the recursion method is too straightforward. 
Use one stack for iteration method, be notice that for preorder, 
push right tree first to stack then left tree, so when stack pop, left tree pop out first then right tree.
 
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
     * @return: Preorder in ArrayList which contains node values.
     */
    vector<int> preorderTraversal(TreeNode * root) {
        vector<int> ans;
        if (root == nullptr) return ans;

        s.push(root);
        while (!s.empty()) {
            TreeNode* cur = s.top();
            s.pop();
            ans.push_back(cur->val);
            if (cur->right) {
                s.push(cur->right);
            }            
            if (cur->left) {
                s.push(cur->left);
            }
        }

        return ans;
    }

private:
    stack<TreeNode*> s;
};
 ```
 