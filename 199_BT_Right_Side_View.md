Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.  

Example 1:  
```
Input: root = [1,2,3,null,5,null,4]
Output: [1,3,4]
```

Example 2:  
```
Input: root = [1,null,3]
Output: [1,3]
```

Example 3:  
```
Input: root = []
Output: []
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
    vector<int> rightSideView(TreeNode* root) {
        view = 0;
        vector<int> rsv;
        if(root) trace(root, 1, rsv);
        return rsv;
    }
    void trace(TreeNode* root, int rank, vector<int>& rsv) {
        if(rank > view) {
            rsv.push_back(root -> val);
            view = rank;
        }
        if(root -> right) trace(root -> right, rank+1, rsv);
        if(root -> left) trace(root -> left, rank+1, rsv);
    }
private:
    int view;
};
```

Runtime: 0 ms, faster than 100% of C++ online submissions.  
Memory Usage: 12 MB, less than 59.70% of C++ online submissions.
