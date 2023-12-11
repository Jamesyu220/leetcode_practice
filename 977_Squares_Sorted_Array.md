Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.  

Example 1:  
```
Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].
```

Example 2:  
```
Input: nums = [-7,-3,2,3,11]
Output: [4,9,9,49,121]
```

Code:  
```c++
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        vector<int> res(nums.size());
        for(int i = 0; i < nums.size(); ++i) {
            nums[i] *= nums[i];
        }
        int l = 0, r = nums.size() - 1;
        int j = 0;
        while(l <= r) {
            if(nums[l] >= nums[r]) {
                res[j] = nums[l];
                ++l;
            }
            else {
                res[j] = nums[r];
                --r;
            }
            ++j;
        }
        reverse(res.begin(), res.end());
        return res;
    }
};
```

Runtime: 24 ms, faster than 63.18% of C++ online submissions.  
Memory Usage: 26.10 MB, less than 99.37% of C++ online submissions.  
