Given an integer array ```nums```, find the subarray with the largest sum, and return its sum.  

Example 1:  
```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: The subarray [4,-1,2,1] has the largest sum 6.
```

Example 2:  
```
Input: nums = [1]
Output: 1
Explanation: The subarray [1] has the largest sum 1.
```

Example 3:  
```
Input: nums = [5,4,-1,7,8]
Output: 23
Explanation: The subarray [5,4,-1,7,8] has the largest sum 23.
```

Constraints:  
```
1 <= nums.length <= 105
-104 <= nums[i] <= 104
```

Code:  
```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int global_max = -10000 * nums.size();
        int local_max = 0;
        bool all_negative = true;
        for(int i = 0; i < nums.size(); ++i) {
            if(nums[i] >= 0) {
                if(all_negative) all_negative = false;
                local_max += nums[i];
                if(i == nums.size() - 1 && local_max > global_max) global_max = local_max; 
            }
            else {
                if(!all_negative){
                    if(local_max > global_max) global_max = local_max;
                    if(local_max + nums[i] > 0) local_max += nums[i];
                    else local_max = 0;
                } 
                else if(nums[i] > global_max) global_max = nums[i];           
            }
        }
        return global_max;
    }
};
```
Runtime: 111 ms, faster than 89.71% of C++ online submissions for Maximum Subarray.  
Memory Usage: 67.7 MB, less than 60.5% of C++ online submissions for Maximum Subarray.
