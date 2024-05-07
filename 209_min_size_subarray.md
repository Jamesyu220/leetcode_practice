Given an array of positive integers nums and a positive integer target, return the minimal length of a subarray whose sum is greater than or equal to target.  
If there is no such subarray, return 0 instead.  

Example 1:  
```
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.
```

Example 2:  
```
Input: target = 4, nums = [1,4,4]
Output: 1
```

Example 3:  
```
Input: target = 11, nums = [1,1,1,1,1,1,1,1]
Output: 0
```

Code:  
```c++
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int min_len = 0;
        int local_min = 0;
        int start = 0;
        int sum = 0;
        for(int i = 0; i < nums.size(); ++i) {
            sum += nums[i];
            while(sum - nums[start] >= target) {
                sum -= nums[start];
                ++start;
            }
            if(sum >= target) {
                local_min = i - start + 1;
                if(min_len == 0 || local_min < min_len) min_len = local_min;
            }
        }
        return min_len;
    }
};
```

Performance:  
Time: 26 ms Beats 62.77% of users with C++.  
Memory: 0.68 MB Beats 15.91% of users with C++.  
