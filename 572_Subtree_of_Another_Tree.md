Given the roots of two binary trees root and subRoot, return true if there is a subtree of root with the same structure and node values of subRoot and false otherwise.  

A subtree of a binary tree tree is a tree that consists of a node in tree and all of this node's descendants. The tree tree could also be considered as a subtree of itself.  

Example 1:  
```
Input: root = [3,4,5,1,2], subRoot = [4,1,2]
Output: true
```

Example 2:  
```
Input: root = [3,4,5,1,2,null,null,null,null,0], subRoot = [4,1,2]
Output: false
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
    bool isSubtree(TreeNode* root, TreeNode* subRoot) {
        if(!root) return false;
        if(root -> val == subRoot -> val && isEqual(root, subRoot)) return true;
        
        return (isSubtree(root -> left, subRoot) || isSubtree(root -> right, subRoot));
    }
    bool isEqual(TreeNode* root1, TreeNode* root2) {
        if(!root1 && !root2) return true;
        else if(!root1 || !root2) return false;
        
        if(root1 -> val != root2 -> val) return false;

        if(!isEqual(root1 -> left, root2 -> left)) return false;
        if(!isEqual(root1 -> right, root2 -> right)) return false;

        return true;
    }
};
```

Runtime: 21 ms, faster than 36.01% of C++ online submissions.  
Memory Usage: 29.16 MB, less than 53.49% of C++ online submissions.
