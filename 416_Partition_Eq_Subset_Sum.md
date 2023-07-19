Given an integer array nums, return true if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or false otherwise.  

Example 1:  
```
Input: nums = [1,5,11,5]
Output: true
Explanation: The array can be partitioned as [1, 5, 5] and [11].
```

Example 2:  
```
Input: nums = [1,2,3,5]
Output: false
Explanation: The array cannot be partitioned into equal sum subsets.
```

Code:  
```c++
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        if(nums.size() == 1) return !nums[0];

        sort(nums.begin(), nums.end());
        int max = nums.back();
        int sum = 0;
        for(int i = 0; i <= nums.size()-2; ++i) sum += nums[i];

        int diff = sum - max;
        if(diff == 0) return true;
        if(diff < 0 || diff % 2 != 0) return false;
        sumN.resize(nums.size()-1);
        return findNum(nums, nums.size()-1, diff/2);
    }
    bool findNum(vector<int>& nums, int i, int n) {
        if(n == 0) return true;
        if(i < 1 || n < 0) return false;
        if(n < sumN[i-1].size() && sumN[i-1][n] <= 1) return sumN[i-1][n];
        if(n >= sumN[i-1].size()) sumN[i-1].resize(n+1, 2);

        int middle, front = 0, back = i;
        if(nums[front] > n) sumN[i-1][n] = 0;
        else if(nums[front] == n) sumN[i-1][n] = 1;
        else if(nums[back-1] >= n) {
            while(front < back - 1) {
                middle = (front + back) / 2;
                if(nums[middle] == n) {
                    sumN[i-1][n] = 1;
                    return true;
                } 
                else if(nums[middle] > n) back = middle;
                else front = middle;
            }
            sumN[i-1][n] = findNum(nums, back, n);
        }
        else sumN[i-1][n] = findNum(nums, back-1, n) || findNum(nums, back-1, n - nums[back-1]);

        return sumN[i-1][n];
    }
private:
    vector<vector<int>> sumN;  // sumN[i, j] = 1 iff we can find some numbers in nums[0:i] that the sum of these numbers is j.
};
```

Runtime: 377 ms, faster than 52.54% of C++ online submissions.  
Memory Usage: 89.3 MB, less than 50.10% of C++ online submissions.
