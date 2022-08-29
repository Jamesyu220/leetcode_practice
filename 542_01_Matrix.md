Given an m x n binary matrix mat, return the distance of the nearest 0 for each cell.  
The distance between two adjacent cells is 1.  

ex:  
Input: mat = [[0,0,0],[0,1,0],[0,0,0]]  
Output: [[0,0,0],[0,1,0],[0,0,0]]  

code:  
C++:  

```c
class Solution {
public:
    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
        int m = mat.size();
        int n = mat[0].size();
        vector<vector<int>> r_mat(m);
        vector<vector<bool>> visited(m);
        for(int i = 0; i < m; ++i) {
            r_mat[i].resize(n);
            visited[i].resize(n);
            for(int j = 0; j < n; ++j) visited[i][j] = false;
        }
        queue<pair<int, int>> q;
        
        // find 0
        for(int i = 0; i < m; ++i) {
            for(int j = 0; j < n; ++j) {
                if(mat[i][j] == 0) {
                    visited[i][j] = true;
                    r_mat[i][j] = 0;
                    pair<int, int> p(i, j);
                    q.push(p);
                }
            }
        }
        
        // propagate
        while(!q.empty()) {
            pair<int, int> cur = q.front();
            int i = cur.first, j = cur.second;
            q.pop();
            if(i > 0) { 
                if(!visited[i-1][j]) {
                    visited[i-1][j] = true;
                    r_mat[i-1][j] = r_mat[i][j] + 1;
                    pair<int, int> new_p(i-1, j);
                    q.push(new_p);
                }              
            }
            if(i < m - 1) {
                if(!visited[i+1][j]) {
                    visited[i+1][j] = true;
                    r_mat[i+1][j] = r_mat[i][j] + 1;
                    pair<int, int> new_p(i+1, j);
                    q.push(new_p);
                }               
            }
            if(j > 0) {
                if(!visited[i][j-1]) {
                    visited[i][j-1] = true;
                    r_mat[i][j-1] = r_mat[i][j] + 1;
                    pair<int, int> new_p(i, j-1);
                    q.push(new_p);
                }                
            }
            if(j < n - 1) {
                if(!visited[i][j+1]) {
                    visited[i][j+1] = true;
                    r_mat[i][j+1] = r_mat[i][j] + 1;
                    pair<int, int> new_p(i, j+1);
                    q.push(new_p);
                }
            }
        }
        return r_mat;
    }
};
```
time: 182 ms  
memory: 32.2 MB
