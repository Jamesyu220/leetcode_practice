You are given an m x n grid where each cell can have one of three values:  
0 representing an empty cell, 1 representing a fresh orange, or 2 representing a rotten orange.  
Every minute, any fresh orange that is 4-directionally adjacent to a rotten orange becomes rotten.  

Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return -1.  

Example 1:  
```
Input: grid = [[2,1,1],[1,1,0],[0,1,1]]
Output: 4
```

Example 2:  
```
Input: grid = [[2,1,1],[0,1,1],[1,0,1]]
Output: -1
Explanation: The orange in the bottom left corner (row 2, column 0) is never rotten, because rotting only happens 4-directionally.
```

Example 3:  
```
Input: grid = [[0,2]]
Output: 0
Explanation: Since there are already no fresh oranges at minute 0, the answer is just 0.
```

Code:  
```c++
class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid) {
        int minute = 0;
        vector<pair<int, int>> rotten, rotting;
        for(int i = 0; i < grid.size(); ++i) {
            for(int j = 0; j < grid[i].size(); ++j) {
                if(grid[i][j] == 2) rotten.push_back(make_pair(i, j));
            }
        }
        int explored = 0;
        while(explored < rotten.size()) {
            for(;explored < rotten.size(); ++explored) {
                int i = rotten[explored].first, j = rotten[explored].second;
                if(i > 0 && grid[i-1][j] == 1) {
                    rotting.push_back(make_pair(i-1, j));
                    grid[i-1][j] = 2;
                } 
                if(i < grid.size() - 1 && grid[i+1][j] == 1) {
                    rotting.push_back(make_pair(i+1, j));
                    grid[i+1][j] = 2;
                } 
                if(j > 0 && grid[i][j-1] == 1) {
                    rotting.push_back(make_pair(i, j-1));
                    grid[i][j-1] = 2;
                } 
                if(j < grid[0].size() - 1 && grid[i][j+1] == 1) {
                    rotting.push_back(make_pair(i, j+1));
                    grid[i][j+1] = 2;
                }
            }
            if(rotting.empty()) break;
            rotten.insert(rotten.end(), rotting.begin(), rotting.end());
            rotting.clear();
            minute ++;
        }
        for(int i = 0; i < grid.size(); ++i) {
            for(int j = 0; j < grid[i].size(); ++j) {
                if(grid[i][j] == 1) return -1;
            }
        }
        return minute;
    }
};
```

Runtime: 11 ms, faster than 38.24% of C++ online submissions.  
Memory Usage: 13.3 MB, less than 30.38% of C++ online submissions.  
