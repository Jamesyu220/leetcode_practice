Given the root of a binary search tree, and an integer k, return the kth smallest value (1-indexed) of all the values of the nodes in the tree.   

Example 1:  
```
Input: root = [3,1,4,null,2], k = 1
Output: 1
```

Example 2:  
```
Input: root = [5,3,6,2,4,null,null,1], k = 3
Output: 3
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
    int kthSmallest(TreeNode* root, int k) {
        pair<int, int> result = matchOrder(root, k, 0);
        return result.first;
    }
    pair<int, int> matchOrder(TreeNode* node, int k, int base) {  // the first int is the k-th value if found, -1 if not found; the second int tell its parent how to modify its order.
        // if the base is 0, meaning that the root is finding the order.
        // if the base is greater than 0, meaning that the root has fully explored the left subtree and found the order, so the base should be root's order.
        int order;

        if(!node -> left) order = base + 1;
        else {
            pair<int, int> left_result = matchOrder(node -> left, k, base);
            if(left_result.first >= 0) return make_pair(left_result.first, 0);
            order = left_result.second + 1;
        }

        if(order == k) return make_pair(node -> val, 0);

        if(!node -> right) return make_pair(-1, order);
        else {
            pair<int, int> right_result = matchOrder(node -> right, k, order);
            if(right_result.first >= 0) return make_pair(right_result.first, 0);
            else return make_pair(-1, right_result.second);
        }
    }
};
```

Performance:  
Time: 10 ms, Beats 81.73% of users with C++.  
Memory: 22.50 MB, Beats 59.98% of users with C++.  
