Given a binary search tree (BST), find the lowest common ancestor (LCA) node of two given nodes in the BST.  

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T  
that has both p and q as descendants (where we allow a node to be a descendant of itself).”  

Code:  
```c
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */

class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        TreeNode* curNode = root;
        while(true) {
            if(curNode -> val == p -> val || curNode -> val == q -> val) break;
            // p, q are in left subtree
            if(curNode -> val > p -> val && curNode -> val > q -> val) curNode = curNode -> left;
            // p, q are in the right subtree
            else if(curNode -> val < p -> val && curNode -> val < q -> val) curNode = curNode -> right;
            // one in left subtree, one in right subtree
            else break;
        }
        return curNode;
    }
};
```
Runtime: 62 ms, faster than 15.29% of C++ online submissions for Lowest Common Ancestor of a Binary Search Tree.  
Memory Usage: 23.3 MB, less than 14.28% of C++ online submissions for Lowest Common Ancestor of a Binary Search Tree.  
