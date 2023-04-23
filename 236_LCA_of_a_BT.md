Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.  

According to the definition of LCA on Wikipedia:  
“The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”  

Example 1:  
```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.
```

Example 2:  
```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
```

Example 3:  
```
Input: root = [1,2], p = 1, q = 2
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
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        pair<TreeNode*, int> tree = containNode(root, p, q);
        return tree.first;
    }
    pair<TreeNode*, int> containNode(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(!root) return make_pair(root, 0);
        pair<TreeNode*, int> leftTree, rightTree;

        // already found p
        if(!p) {
            if(root -> val == q -> val) return make_pair(root, 1);
            leftTree = containNode(root -> left, NULL, q);
            rightTree = containNode(root -> right, NULL, q);
            if(leftTree.second == 1 || rightTree.second == 1) return make_pair(root, 1);
            else return make_pair(root, 0);
        }

        // already found q
        if(!q) {
            if(root -> val == p -> val) return make_pair(root, 1);
            leftTree = containNode(root -> left, p, NULL);
            rightTree = containNode(root -> right, p, NULL);
            if(leftTree.second == 1 || rightTree.second == 1) return make_pair(root, 1);
            else return make_pair(root, 0);
        }
        
        // both not found
        // root == p
        if(root -> val == p -> val) {
            leftTree = containNode(root -> left, NULL, q);
            rightTree = containNode(root -> right, NULL, q);
            if(leftTree.second == 1 || rightTree.second == 1) return make_pair(root, 2);
            else return make_pair(root, 1);
        }
        // root == q
        if(root -> val == q -> val) {
            leftTree = containNode(root -> left, p, NULL);
            rightTree = containNode(root -> right, p, NULL);
            if(leftTree.second == 1 || rightTree.second == 1) return make_pair(root, 2);
            else return make_pair(root, 1);
        }

        // root not p nor q
        leftTree = containNode(root -> left, p, q);
        rightTree = containNode(root -> right, p, q);
        if(leftTree.second == 2) return leftTree;
        if(rightTree.second == 2) return rightTree;
        if(leftTree.second == 1 && rightTree.second == 1) return make_pair(root, 2);
        if(leftTree.second == 1 || rightTree.second == 1) return make_pair(root, 1);
        return make_pair(root, 0); 
    }
};
```

Runtime: 18 ms, faster than 48.38% of C++ online submissions.  
Memory Usage: 20.7 MB, less than 6.25% of C++ online submissions.
