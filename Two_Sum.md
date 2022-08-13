code:
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
