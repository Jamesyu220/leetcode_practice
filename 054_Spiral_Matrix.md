Given an ```m x n``` matrix, return all elements of the matrix in spiral order.  

Example 1:  
```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```

Example 2:  
```
Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```

Code:  
```c++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int m = matrix.size();
        int n = matrix[0].size();
        int i = 0, j = -1;
        int direction = 0;      // 0: right; 1: down; 2: left; 3: up

        vector<int> elements;
        elements.reserve(m*n);
        while(m > 0 && n > 0) {
            switch(direction) {
                case 0:
                    for(int k = 0; k < n; ++k) {
                        j++;
                        elements.push_back(matrix[i][j]);
                    }
                    m--;
                    direction++;
                    break;
                case 1:
                    for(int k = 0; k < m; ++k) {
                        i++;
                        elements.push_back(matrix[i][j]);
                    }
                    n--;
                    direction++;
                    break;
                case 2:
                    for(int k = 0; k < n; ++k) {
                        j--;
                        elements.push_back(matrix[i][j]);
                    }
                    m--;
                    direction++;
                    break;
                case 3:
                    for(int k = 0; k < m; ++k) {
                        i--;
                        elements.push_back(matrix[i][j]);
                    }
                    n--;
                    direction = 0;
                    break;
            }
        }
        return elements;
    }
};
```

Runtime: 0 ms, faster than 100% of C++ online submissions.  
Memory Usage: 6.7 MB, less than 93.80% of C++ online submissions.
