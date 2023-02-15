Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.vv

Note that you must do this in-place without making a copy of the array.  

Example 1:  
```
Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]
```
Example 2:  
```
Input: nums = [0]
Output: [0]
```
Code:  
```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int numZero = 0;
        for(int i = 0; i < nums.size(); ++i) {
            if(nums[i] == 0) numZero ++;
            else             nums[i - numZero] = nums[i];
        }
        for(int i = nums.size() - numZero; i < nums.size(); ++i) nums[i] = 0;
    }
};
```
Runtime: 28 ms, faster than 51.84% of C++ online submissions for Move Zeroes.  
Memory Usage: 19.3 MB, less than 17.32% of C++ online submissions for Move Zeroes.  
