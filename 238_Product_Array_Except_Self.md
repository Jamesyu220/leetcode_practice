Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].  

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.  

You must write an algorithm that runs in O(n) time and without using the division operation.  

Example 1:  
```
Input: nums = [1,2,3,4]
Output: [24,12,8,6]
```

Example 2:  
```
Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
```

Code:  
```c++
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        vector<int> front(nums.size(), 1), back(nums.size(), 1);
        front[0] = nums[0];
        back[nums.size() - 1] = nums.back();
        for(int i = 1; i < nums.size(); ++i) {
            front[i] = front[i-1] * nums[i];
            back[nums.size() - 1 - i] = back[nums.size() - i] * nums[nums.size() - 1 - i];
        }
        vector<int> answer(nums.size());
        answer[0] = back[1];
        answer[nums.size() - 1] = front[nums.size() - 2];
        for(int i = 1; i < nums.size() - 1; ++i) answer[i] = front[i-1] * back[i+1];
        return answer;
    }
};
```

Runtime: 25 ms, faster than 71.61% of C++ online submissions.  
Memory Usage: 25.2 MB, less than 13.27% of C++ online submissions.
