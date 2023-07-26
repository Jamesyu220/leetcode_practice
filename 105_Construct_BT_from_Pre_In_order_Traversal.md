Given two integer arrays preorder and inorder where preorder is the preorder traversal of a binary tree and inorder is the inorder traversal of the same tree, construct and return the binary tree.  

Example 1:  
```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```

Example 2:  
```
Input: preorder = [-1], inorder = [-1]
Output: [-1]
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
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder, int start_pre = 0, int start_in = 0, int end_in = 0) {
        if(end_in == 0) end_in = inorder.size();
        int i = find(inorder.begin() + start_in, inorder.begin() + end_in, preorder[start_pre]) - inorder.begin() - start_in;
        TreeNode *_left = NULL, *_right = NULL;
        if(i > 0) _left = buildTree(preorder, inorder, start_pre + 1, start_in, start_in + i);
        if(i < end_in - start_in - 1) _right = buildTree(preorder, inorder, start_pre + i + 1, start_in + i + 1, end_in);
        TreeNode* n = new TreeNode(preorder[start_pre], _left, _right);

        return n;
    }
};
```

Runtime: 17 ms, faster than 78.15% of C++ online submissions.  
Memory Usage: 25.9 MB, less than 71.89% of C++ online submissions.
