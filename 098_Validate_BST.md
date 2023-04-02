Given the root of a binary tree, determine if it is a valid binary search tree (BST).  

A valid BST is defined as follows:  
The left subtree of a node contains only nodes with keys less than the node's key.  
The right subtree of a node contains only nodes with keys greater than the node's key.  
Both the left and right subtrees must also be binary search trees.  

Example 1:  
```
Input: root = [2,1,3]
Output: true
```

Example 2:  
```
Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
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
    bool isValidBST(TreeNode* root) {
        return validBST(root).first;
    }
    pair<bool, pair<int, int>> validBST(TreeNode* root) {
        pair<int, int> maxmin = make_pair(root -> val, root -> val);
        if(!root -> left && !root -> right) return make_pair(true, maxmin);
        pair<bool, pair<int, int>> leftSub, rightSub;
        if(root -> left) {
            leftSub = validBST(root -> left);
            if(!leftSub.first || root -> val <= leftSub.second.first) return make_pair(false, make_pair(0, 0));
            maxmin.second = leftSub.second.second;           
        }
        if(root -> right) {
            rightSub = validBST(root -> right);
            if(!rightSub.first || root -> val >= rightSub.second.second) return make_pair(false, make_pair(0, 0));
            maxmin.first = rightSub.second.first;           
        }
        return make_pair(true, maxmin);
    }
};
```

Runtime: 15 ms, faster than 47.74% of C++ online submissions.  
Memory Usage: 22.3 MB, less than 13.8% of C++ online submissions.  
