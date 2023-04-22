Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.  

Example 1:  
```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

Example 2:  
```
Input: nums = [0,1]
Output: [[0,1],[1,0]]
```

Example 3:  
```
Input: nums = [1]
Output: [[1]]
```

Code:  
```c++
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> permutation, subpermutation;
        for(int i = 0; i < nums.size(); ++i) {
            subpermutation = recursive(nums, {nums[i]});
            permutation.insert(permutation.end(), subpermutation.begin(), subpermutation.end());
        }
        return permutation;
    }
    vector<vector<int>> recursive(vector<int>& nums, vector<int> subnums) {
        vector<vector<int>> permutation;
        if(nums.size() == subnums.size()) {
            permutation.push_back(subnums);
            return permutation;
        }
        vector<vector<int>> subpermutation;
        for(int i = 0; i < nums.size(); ++i) {
            if(find(subnums.begin(), subnums.end(), nums[i]) != subnums.end()) continue;
            subnums.push_back(nums[i]);
            subpermutation = recursive(nums, subnums);
            permutation.insert(permutation.end(), subpermutation.begin(), subpermutation.end());
            subnums.pop_back();
        }
        return permutation;
    }
};
```

Runtime: 10 ms, faster than 7.49% of C++ online submissions.  
Memory Usage: 10 MB, less than 5.16% of C++ online submissions.
