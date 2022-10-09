Given an array nums of size n, return the majority element.  

The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.  

Code:  
```C++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int n = nums.size();
        if(n == 1) return nums[0];
        int majority;
        map<int, int> freq;
        for(int i = 0; i < n; ++i) {
            if(freq.count(nums[i]) > 0) freq[nums[i]] ++;
            else freq[nums[i]] = 1;
            
            if(freq[nums[i]] > n/2) {
                majority = nums[i];
                break;
            }
        }
        return majority;
    }
};
```
Runtime: 27 ms, faster than 75.01% of C++ online submissions for Majority Element.  
Memory Usage: 19.7 MB, less than 14.66% of C++ online submissions for Majority Element.  
