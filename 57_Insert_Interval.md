Problem:  
You are given an array of non-overlapping intervals intervals where intervals[i] = [starti, endi] represent the start and the end of the ith interval and intervals is sorted in ascending order by starti. You are also given an interval newInterval = [start, end] that represents the start and end of another interval.

Insert newInterval into intervals such that intervals is still sorted in ascending order by starti and intervals still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return intervals after the insertion.  

Code:  
C++:  
```c
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        int size = intervals.size();
        int start =size, end = size;
        vector<vector<int>>::iterator it = intervals.begin();
        for(int i = 0; i < size; ++i) {
            if(intervals[i][1] >= newInterval[0]) {if(start == size) start = i;}
            else continue;
            if(intervals[i][0] > newInterval[1]) {
                end = i;
                break;
            }
        }
        if(start == end) intervals.insert(it + start, newInterval);
        else {
            vector<int> insert_v(2);
            insert_v[0] = (newInterval[0] < intervals[start][0])? newInterval[0]: intervals[start][0];
            insert_v[1] = (newInterval[1] > intervals[end - 1][1])? newInterval[1]: intervals[end - 1][1];
            intervals.erase(it + start, it + end);
            intervals.insert(it + start, insert_v);
        }
        return intervals;
    }
};
```
