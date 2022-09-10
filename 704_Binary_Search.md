Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums.  
If target exists, then return its index. Otherwise, return -1.  

You must write an algorithm with O(log n) runtime complexity.  

Code:  
```python
class Solution(object):
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        front = 0
        back = len(nums) - 1
        
        while True:
            middle = (front + back) / 2
            if nums[middle] == target:
                return middle         
            elif front == middle:
                if nums[back] == target:
                    return back
                else:
                    return -1
            elif nums[middle] > target:
                back = middle
            else:
                front = middle
```
Runtime: 246 ms, faster than 72.26% of Python online submissions for Binary Search.  
Memory Usage: 14.5 MB, less than 94.60% of Python online submissions for Binary Search.  
