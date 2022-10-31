Given the root of a binary tree, return its maximum depth.  

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.  

Example 1:
```
Input: root = [3,9,20,null,null,15,7]
Output: 3
```
Example 2:
```
Input: root = [1,null,2]
Output: 2
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
    int maxDepth(TreeNode* root) {
        if(!root) return 0;
        if(!root -> left) return maxDepth(root -> right) + 1;
        else if(!root -> right) return maxDepth(root -> left) + 1;
        else {
            int left_depth, right_depth;
            left_depth = maxDepth(root -> left);
            right_depth = maxDepth(root -> right);
            if(left_depth >= right_depth) return left_depth + 1;
            else return right_depth + 1;
        }
    }
};
```

Runtime: 3 ms, faster than 99.45% of C++ online submissions for Maximum Depth of Binary Tree.  
Memory Usage: 19 MB, less than 14.27% of C++ online submissions for Maximum Depth of Binary Tree.
