Given a binary tree, determine if it is height-balanced.  

For this problem, a height-balanced binary tree is defined as:  

a binary tree in which the left and right subtrees of every node differ in height by no more than 1.  

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
    bool isBalanced(TreeNode* root) {
        if(!root) return true;
        pair<int, bool> leftNode = balancedNode(root -> left);
        pair<int, bool> rightNode = balancedNode(root -> right);
        if(!leftNode.second) return false;
        if(!rightNode.second) return false;
        int left_h = leftNode.first;
        int right_h = rightNode.first;
        if(left_h > right_h + 1 || left_h < right_h - 1) return false;
        return true;
    }
    pair<int, bool> balancedNode(TreeNode* root) {
        if(!root) return make_pair(0, true);
        pair<int, bool> leftNode = balancedNode(root -> left);
        pair<int, bool> rightNode = balancedNode(root -> right);
        if(!leftNode.second) return make_pair(0, false);
        if(!rightNode.second) return make_pair(0, false);
        int left_h = leftNode.first;
        int right_h = rightNode.first;
        if(left_h > right_h + 1 || left_h < right_h - 1) return make_pair(0, false);
        else if(left_h >= right_h) return make_pair(left_h + 1, true);
        else return make_pair(right_h + 1, true);
    }
};
```

Runtime: 32 ms, faster than 18.51% of C++ online submissions for Balanced Binary Tree.  
Memory Usage: 20.8 MB, less than 81.01% of C++ online submissions for Balanced Binary Tree.  
