Given an ```m x n``` grid of characters board and a string word, return true if word exists in the grid.  

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.  

Example 1:  
```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
```

Example 2:  
```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
Output: true
```

Example 3:  
```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
Output: false
```

Code:  
```c++
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        int m = board.size(), n = board[0].size();
        for(int p = 0; p < m; ++p) {
            for(int q = 0; q < n; ++q) {
                if(board[p][q] == word[0] && DFS(board, word, p, q, 1)) {
                    return true;
                }
            }
        }
        return false;
    }
    bool DFS(vector<vector<char>>& board, string& word, int x, int y, int i) {
        if(i == word.size()) return true;

        char currChar = board[x][y];
        board[x][y] = ' ';
        bool up = false, down = false, left = false, right = false;
        if(x > 0 && board[x-1][y] == word[i]) {
            up = DFS(board, word, x-1, y, i+1);
        }
        if(x < board.size() - 1 && board[x+1][y] == word[i]) {
            down = DFS(board, word, x+1, y, i+1);
        }
        if(y > 0 && board[x][y-1] == word[i]) {
            left = DFS(board, word, x, y-1, i+1);
        }
        if(y < board[0].size() - 1 && board[x][y+1] == word[i]) {
            right = DFS(board, word, x, y+1, i+1);
        }
        board[x][y] = currChar;
        return (up || down || left || right);
    }
};
```

Runtime: 209 ms, faster than 95.32% of C++ online submissions.  
Memory Usage: 8.4 MB, less than 43.62% of C++ online submissions.  
