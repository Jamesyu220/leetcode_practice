Given the root of a binary tree, invert the tree, and return its root.  
Code:  
```c
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if(!root) return NULL;
        if(!root -> left) {
            root -> left = invertTree(root -> right);
            root -> right = NULL;
        }
        else if(!root -> right) {
            root -> right = invertTree(root -> left);
            root -> left = NULL;
        }
        else {
            TreeNode* tempNode = invertTree(root -> left);
            root -> left = invertTree(root -> right);
            root -> right = tempNode;
        }
        return root;
    }
};
```
Runtime: 0 ms, faster than 100.00% of C++ online submissions for Invert Binary Tree.  
Memory Usage: 9.6 MB, less than 79.73% of C++ online submissions for Invert Binary Tree.  
