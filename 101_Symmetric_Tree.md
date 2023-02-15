Given the root of a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).  

Example 1:  
```
Input: root = [1,2,2,3,4,4,3]
Output: true
```
Example 2:  
```
Input: root = [1,2,2,null,3,null,3]
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
    bool isSymmetric(TreeNode* root) {
        return isMirror(root -> left, root -> right);
    }
    bool isMirror(TreeNode* t1, TreeNode* t2) {
        if(!t1 && !t2) return true;
        if((!t1 && t2) || (t1 && !t2)) return false;
        if(t1 -> val != t2 -> val) return false;
        if((t1 -> left && !t2 -> right) || (!t1 -> left && t2 -> right) || (t1 -> right && !t2 -> left) || (!t1 -> right && t2 -> left)) return false;
        return isMirror(t1 -> left, t2 -> right) && isMirror(t1 -> right, t2 -> left);
    }
};
```

Runtime: 0 ms, faster than 100% of C++ online submissions for Symmetric Tree.  
Memory Usage: 16.4 MB, less than 58.14% of C++ online submissions for Symmetric Tree.  
