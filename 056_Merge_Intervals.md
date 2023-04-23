Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals,  
and return an array of the non-overlapping intervals that cover all the intervals in the input.  

Example 1:  
```
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].
```

Example 2:  
```
Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```

Code:  
```c++
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        int max_start = 0;
        for(int i = 0; i < intervals.size(); ++i) {
            if(intervals[i][0] > max_start) max_start = intervals[i][0];
        }
        vector<int> intervalTable(max_start + 1, -1);
        // index of table represents the start of intervals, while the content of table represents the end of intervals.
        for(int i = 0; i < intervals.size(); ++i) {
            if(intervalTable[intervals[i][0]] < intervals[i][1]) intervalTable[intervals[i][0]] = intervals[i][1];
        }

        int unmerged_region = 0; // the start of unmerged region
        vector<vector<int>> mergedIntervals;
        while(unmerged_region <= max_start) {
            while(intervalTable[unmerged_region] < 0) ++ unmerged_region;
            int max = intervalTable[unmerged_region];    // max end of overlapped regions
            for(int i = unmerged_region + 1; i <= max_start && i <= max; ++i) {
                if(intervalTable[i] > max) max = intervalTable[i];
            }
            mergedIntervals.push_back({unmerged_region, max});
            unmerged_region = max + 1;
        }
        return mergedIntervals;
    }
};
```

Runtime: 24 ms, faster than 99.7% of C++ online submissions.  
Memory Usage: 19.2 MB, less than 49.72% of C++ online submissions.
