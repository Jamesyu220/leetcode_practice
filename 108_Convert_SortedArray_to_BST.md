Given an integer array ```nums``` where the elements are sorted in ascending order, convert it to a height-balanced binary search tree.  

Example 1:  
```
Input: nums = [-10,-3,0,5,9]
Output: [0,-3,9,-10,null,5]
Explanation: [0,-10,5,null,-3,null,9] is also accepted:
```

Example 2:  
```
Input: nums = [1,3]
Output: [3,1]
Explanation: [1,null,3] and [3,1] are both height-balanced BSTs.
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
    TreeNode* sortedArrayToBST(vector<int>& nums, int start = 0, int end = 0) {
        if(end == 0) end = nums.size();

        TreeNode* n = NULL;
        if(start == end - 1) {
            n = new TreeNode(nums[start]);
            return n;
        }

        TreeNode *_left = NULL, *_right = NULL;
        int middle = (start + end) / 2;
        if(middle > start) _left = sortedArrayToBST(nums, start, middle);
        if(middle + 1 < end) _right = sortedArrayToBST(nums, middle+1, end);
        n = new TreeNode(nums[middle], _left, _right);
        return n;
    }
};
```
Runtime: 8 ms, beats 94.28% of users with C++.  
Memory: 21.3 mb, beats 57.24% of users with C++.
