There is an integer array nums sorted in ascending order (with distinct values).  
Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed).  
For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].  
Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.  
You must write an algorithm with O(log n) runtime complexity.  

Example 1:  
```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

Example 2:  
```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

Example 3:  
```
Input: nums = [1], target = 0
Output: -1
```

Code:  
```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int front, back = nums.size() - 1;
        int max = 0;
        if(nums[0] <= nums.back()) max = nums.size() - 1;
        else {
            while(nums[max] < nums[max+1]) {
                if(nums[(max + back) / 2] > nums[back]) max = (max + back) / 2;
                else back = (max + back) / 2;
            }
        }

        if(target == nums[0]) return 0;
        else if(target > nums[0] || max == nums.size() - 1) {
            front = 0;
            back = max;
        }
        else {
            front = max + 1;
            back = nums.size() - 1;
        }

        if(nums[front] > target || nums[back] < target) return -1;
        if(nums[front] == target) return front;
        if(nums[back] == target) return back;

        while(front < back - 1) {
            int middle = (front + back) / 2;
            if(nums[middle] == target) return middle;
            else if(nums[middle] < target) front = middle;
            else back = middle;
        }
        return -1;
    }
};
```

Runtime: 5 ms, faster than 47.21% of C++ online submissions.  
Memory Usage: 11.2 MB, less than 6.65% of C++ online submissions.  
