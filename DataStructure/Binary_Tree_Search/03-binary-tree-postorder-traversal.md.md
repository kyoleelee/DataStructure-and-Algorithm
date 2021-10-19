# Binary Tree Postorder Traversal
> Source: LintCode (https://www.lintcode.com/problem/68/)
## Problem Description
```
Given a binary tree, return the postorder traversal of its nodes’ values.

    The first data is the root node, followed by the value of the left and right son nodes, and "#" indicates that there is no child node.
    The number of nodes does not exceed 20.

Example

Example 1:

Input:

binary tree = {1,2,3}

Output:

[2,3,1]

Explanation:

   1
/  \
2     3
It will be serialized to {1,2,3} followed by post-order traversal

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
It will be serialized to {1,#,2,3} followed by post-order traversal
Challenge

Can you do it without recursion?

```

 ### C++ Solution
Do it with iteration, because the recursion method is too straightforward. 
Use one stack for iteration method, see code comment for details of each case.
 
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
     * @return: Postorder in ArrayList which contains node values.
     */
    vector<int> postorderTraversal(TreeNode * root) {
        vector<int> ans;
        if (root == nullptr) return ans;

        s.push(root);
        TreeNode* prev = nullptr;

        while (!s.empty()) {
            TreeNode* cur = s.top(); // get the current node from stack

            // case 1: prev is null or prev is parent of current node
            // this is the 1st visit of current node, go left tree
            if (prev == nullptr || prev->left == cur || prev->right == cur) {
                if (cur->left != nullptr) {
                    s.push(cur->left);
                }
                else if (cur->right != nullptr) {
                    s.push(cur->right);
                }
            }
            // case 2: prve is current node's left tree
            // this is the 2nd visit of current node, go right tree 
            else if (prev == cur->left) {
                if (cur->right != nullptr) {
                    s.push(cur->right);
                }
            }
            // case 3: prev is curent node's right tree
            // this is the 3rd visit of currnt node, record the node value to ans, pop node from stack
            else {
                ans.push_back(cur->val);
                s.pop();
            }

            prev = cur; // udpate prev with cur
        }

        return ans;
    }

private:
    stack<TreeNode*> s;
};
 ```
 