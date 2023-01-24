Given the roots of two binary trees p and q, write a function to check if they are the same or not.  

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.  

Example 1:  
```
Input: p = [1,2,3], q = [1,2,3]
Output: true
```

Example 2:  
```
Input: p = [1,2], q = [1,null,2]
Output: false
```

Example 3:  
```
Input: p = [1,2,1], q = [1,1,2]
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
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if(!p && !q) return true;
        else if(!p || !q) return false;

        if(p -> val != q -> val) return false;

        bool left_same, right_same;
        left_same  = isSameTree(p -> left , q -> left );
        if(!left_same) return false;
        
        right_same = isSameTree(p -> right, q -> right);
        if(right_same) return true;
        else           return false;
    }
};
```
Runtime: 3 ms, faster than 57.53% of C++ online submissions for Same Tree.  
Memory Usage: 10.1 MB, less than 8.69% of C++ online submissions for Same Tree.
