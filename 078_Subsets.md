Given an integer array nums of unique elements, return all possible subsets (the power set).  

The solution set must not contain duplicate subsets. Return the solution in any order.  

Example 1:  
```
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```

Example 2:  
```
Input: nums = [0]
Output: [[],[0]]
```

Code:  
```c++
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> output;
        output.reserve(1 << nums.size());
        output.push_back({});
        for(int i = 0; i < nums.size(); ++i) {
            int k = output.size();
            for(int j = 0; j < k; ++j) {
                vector<int> newSet = output[j];
                newSet.push_back(nums[i]);
                output.push_back(newSet);
            }
        }
        return output;
    }
};
```

Runtime: 6 ms, faster than 27.97% of C++ online submissions.  
Memory Usage: 7 MB, less than 91.55% of C++ online submissions.  

```python
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        sol = []
        size = len(nums)
        for i in range(2**size):
            sol.append([])
            for j in range(size):
                if (i / (2**j)) % 2 == 1:
                    sol[i].append(nums[j])
        
        return sol
```

Runtime: 18 ms, faster than 72.84% of Python online submissions.  
Memory Usage: 13.7 MB, less than 12.7% of Python online submissions.
