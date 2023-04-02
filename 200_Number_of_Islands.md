Given an ```m x n``` 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands.  

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically.  
You may assume all four edges of the grid are all surrounded by water.  

Example 1:  
```
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
```

Example 2:  
```
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```

Code:  
```c++
class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        int num = 0;

        for(int i = 0; i < grid.size(); ++i) {
            for(int j = 0; j < grid[i].size(); ++j) {
                if(grid[i][j] == '1') {
                    num ++;
                    explore(grid, i, j);
                }
            }
        }

        return num;
    }
    void explore(vector<vector<char>>& grid, int i, int j) {
        grid[i][j] = '2';
        if(i > 0 && grid[i-1][j] == '1')                    explore(grid, i-1, j);
        if(i < grid.size() - 1 && grid[i+1][j] == '1')      explore(grid, i+1, j);
        if(j > 0 && grid[i][j-1] == '1')                    explore(grid, i, j-1);
        if(j < grid[0].size() - 1 && grid[i][j+1] == '1')   explore(grid, i, j+1);
    }
};
```

Runtime: 33 ms, faster than 89.29% of C++ online submissions.  
Memory Usage: 12.4 MB, less than 65.29% of C++ online submissions.  
