Given an array of integers ```nums``` and an integer ```target```, return indices of the two numbers such that they add up to ```target```.  
You may assume that each input would have exactly one solution, and you may not use the same element twice.  
You can return the answer in any order.  

Example 1:  
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

Example 2:  
```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

Example 3:  
```
Input: nums = [3,3], target = 6
Output: [0,1]
```
 
Code:  
C++:  
```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        sortedNums = nums;
        sort(sortedNums.begin(), sortedNums.end());
        int first, second;
        for(int i = 0; i < sortedNums.size()-1; ++i) {
            if(target % 2 == 0 && sortedNums[i] == target / 2) {
                first = find(nums.begin(), nums.end(), sortedNums[i]) - nums.begin();
                second = find(nums.begin()+first+1, nums.end(), sortedNums[i]) - nums.begin();
                break;
            }
            if(findNum(i+1, target-sortedNums[i])) {
                first = find(nums.begin(), nums.end(), sortedNums[i]) - nums.begin();
                second = find(nums.begin(), nums.end(), target - sortedNums[i]) - nums.begin();
                break;
            }
        }
        return {first, second};
    }
private:
    vector<int> sortedNums;
    bool findNum(int start, int target) {
        int front = start, back = sortedNums.size();
        if(sortedNums[front] == target) return true;
        while(front < back - 1) {
            int middle = (front + back) / 2;
            if(sortedNums[middle] == target) return true;
            else if(sortedNums[middle] > target) back = middle;
            else front = middle;
        }
        return false;
    }
};
```

Runtime: 7ms, beats 96.72% of users with C++.  
Memory: 10.40mb, beats 52.78% of users with C++.  

Python:  
```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        temp = sorted(nums)
        half = target/2
        if target % 2 == 0:
            if half in nums:
                first = nums.index(half)
                if half in nums[first+1:]:
                    second = first + 1 + nums[first+1:].index(half)
                    return [first, second]
        for i in range(len(temp)):
            if temp[i] > half:
                middle = i
                break
        back = temp[middle:]
        for i in range(middle):
            if (target - temp[i]) in back:
                return [nums.index(temp[i]), nums.index(target-temp[i])]
```

Runtime: 68ms, beats 58.61% of users with Python.  
Memory: 14mb, beats 91.57% of users with Python.  
