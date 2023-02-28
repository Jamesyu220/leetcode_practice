There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1.  
You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.  

For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.  
Return true if you can finish all courses. Otherwise, return false.  

Example 1:  
```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.
```
Example 2:  
```
Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
```

Code:  
```c++
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        // initialization
        ini(numCourses);
        // building adjacency list
        for(int i = 0; i < prerequisites.size(); ++i) preReqList[prerequisites[i][0]].push_back(prerequisites[i][1]);
        // check cycles
        for(int i = 0; i < numCourses; ++i) {
            if(status[i] == 0) {
                if(haveCycle(i)) return false;
            }
        }
        return true;
    }
    void ini(int numCourses) {
        preReqList.resize(numCourses);
        status.resize(numCourses);
        for(int i = 0; i < numCourses; i++) status[i] = 0;
    } 
    bool haveCycle(int course) {
        status[course] = 1;
        for(int i = 0; i < preReqList[course].size(); ++i) {
            if(status[preReqList[course][i]] == 1) return true;
            if(status[preReqList[course][i]] == 0) {
                if(haveCycle(preReqList[course][i])) return true;
            }
        }
        status[course] = 2;
        return false;
    }
private:
    vector<vector<int>> preReqList;
    vector<int> status;     // 0: unvisited; 1: visited; 2: finished
};
```

Runtime: 12 ms, faster than 99.39% of C++ online submissions.  
Memory Usage: 13.2 MB, less than 86.72% of C++ online submissions.
