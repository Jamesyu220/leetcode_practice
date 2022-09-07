Given the nodes of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).  
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
    vector<vector<int>> levelOrder(TreeNode* root) {
        if(root == NULL) return output;
        traverseTree(root, 0);
        return output;
    }
    void traverseTree(TreeNode* root, int level) {
        if(level >= output.size()) output.push_back({});
        output[level].push_back(root -> val);
        if(root -> left != NULL) traverseTree(root -> left, level + 1);
        if(root -> right != NULL) traverseTree(root -> right, level + 1);
    }
private:
    vector<vector<int>> output;
};
```
Runtime: 6 ms, faster than 59.88% of C++ online submissions for Binary Tree Level Order Traversal.  
Memory Usage: 13.7 MB, less than 6.85% of C++ online submissions for Binary Tree Level Order Traversal.  
