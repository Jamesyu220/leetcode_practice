Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.  

You must implement a solution with a linear runtime complexity and use only constant extra space.  

Example 1:  
```
Input: nums = [2,2,1]
Output: 1
```
Example 2:  
```
Input: nums = [4,1,2,1,2]
Output: 4
```
Example 3:  
```
Input: nums = [1]
Output: 1
```

Code:  
```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int singleNum = 0;
        for(int i = 0; i < nums.size(); ++i) singleNum ^= nums[i];
        
        return singleNum;
    }
};
```

Runtime: 21 ms, faster than 66.55% of C++ online submissions for Single Number.  
Memory Usage: 17 MB, less than 55.89% of C++ online submissions for Longest Single Number.  
