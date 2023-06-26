Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent,  
with the colors in the order red, white, and blue.  

We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.  

You must solve this problem without using the library's sort function.  

Code:  
```c++
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int num0 = 0, num1 = 0, num2 = 0;
        for(int i = 0; i < nums.size(); ++i) {
            if(nums[i] == 0) {
                // swap nums[i] and nums[num0]
                nums[i] = nums[num0];
                nums[num0] = 0;
                ++num0;
            }
        }
        for(int i = num0; i < nums.size(); ++i) {
            if(nums[i] == 1) {
                // swap nums[i] and nums[num0 + num1]
                nums[i] = nums[num0 + num1];
                nums[num0 + num1] = 1;
                ++num1;
            }
        }
    }
};
```

Runtime: 0 ms, faster than 100% of C++ online submissions.  
Memory Usage: 8.2 MB, less than 41.94% of C++ online submissions.  
