Given the root of a binary tree, return the length of the diameter of the tree.  

The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.  

The length of a path between two nodes is represented by the number of edges between them.  

Example 1  
```
Input: root = [1,2,3,4,5]
Output: 3
Explanation: 3 is the length of the path [4,2,1,3] or [5,2,1,3].
```
Example 2:
```
Input: root = [1,2]
Output: 1
```
Code:  
```c++
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
    int diameterOfBinaryTree(TreeNode* root) {
        int le_h, ri_h, le_d, ri_d;
        if(!root -> left) {
            if(!root -> right) return 0;
            ri_h = nodeHeight(root -> right);
            ri_d = diameterOfBinaryTree(root -> right);
            if(ri_d >= ri_h + 1) return ri_d;
            else return ri_h + 1;
        }
        else if(!root -> right) {
            le_h = nodeHeight(root -> left);
            le_d = diameterOfBinaryTree(root -> left);
            if(le_d >= le_h + 1) return le_d;
            else return le_h + 1;
        }
        else {
            le_h = nodeHeight(root -> left);
            le_d = diameterOfBinaryTree(root -> left);
            ri_h = nodeHeight(root -> right);
            ri_d = diameterOfBinaryTree(root -> right);
            int diameter = le_h + 2 + ri_h;
            if(diameter >= le_d && diameter >= ri_d) return diameter;
            else if(le_d >= ri_d) return le_d;
            else return ri_d;
        }
    }
    int nodeHeight(TreeNode* root) {
        if(!root -> left) {
            if(!root -> right) return 0;
            return nodeHeight(root -> right) + 1;
        }
        else if(!root -> right) return nodeHeight(root -> left) + 1;
        else {
            int le = nodeHeight(root -> left), ri = nodeHeight(root -> right);
            if(le >= ri) return le + 1;
            else return ri + 1;
        }
    }
};
```

Runtime: 42 ms, faster than 8.81% of C++ online submissions for Diameter of Binary Tree.  
Memory Usage: 20.3 MB, less than 64.43% of C++ online submissions for Diameter of Binary Tree.  
