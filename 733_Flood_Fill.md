An image is represented by an m x n integer grid image where image[i][j] represents the pixel value of the image.  

You are also given three integers sr, sc, and color. You should perform a flood fill on the image starting from the pixel image[sr][sc].  

To perform a flood fill, consider the starting pixel, plus any pixels connected 4-directionally to the starting pixel of the same  
color as the starting pixel, plus any pixels connected 4-directionally to those pixels (also with the same color), and so on.  
Replace the color of all of the aforementioned pixels with color.  

Return the modified image after performing the flood fill.  

Code:  
```c
class Solution {
public:
    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int color) {
        int oriColor = image[sr][sc];
        if(oriColor == color) return image;
        queue<pair<int, int>> neighbors;
        neighbors.push(make_pair(sr, sc));
        while(!neighbors.empty()) {
            pair<int, int> curNode = neighbors.front();
            neighbors.pop();
            int i = curNode.first, j = curNode.second;
            if(image[i][j] != oriColor) continue;
            image[i][j] = color;
            if(i > 0) {
                if(image[i-1][j] == oriColor) neighbors.push(make_pair(i-1, j));            
            }
            if(i < image.size() - 1) {
                if(image[i+1][j] == oriColor) neighbors.push(make_pair(i+1, j));             
            }
            if(j > 0) {
                if(image[i][j-1] == oriColor) neighbors.push(make_pair(i, j-1));             
            }
            if(j < image[0].size() - 1) {
                if(image[i][j+1] == oriColor) neighbors.push(make_pair(i, j+1));             
            }
        }
        return image;
    }
};
```
Runtime: 18 ms, faster than 38.52% of C++ online submissions for Flood Fill.  
Memory Usage: 14.1 MB, less than 34.52% of C++ online submissions for Flood Fill.  
