Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.  

Example 1:
```
Input: nums = [1,2,3,1]
Output: true
```
Example 2:
```
Input: nums = [1,2,3,4]
Output: false
```
Example 3:
```
Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true
```
Code:  
```c++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        for(int i = 0; i < nums.size() - 1; ++i) {
            if(nums[i] == nums[i+1]) return true;
        }
        return false;
    }
};
```

Runtime: 242 ms, faster than 28.77% of C++ online submissions for Contains Duplicate.  
Memory Usage: 46.5 MB, less than 92.59% of C++ online submissions for Contains Duplicate.
