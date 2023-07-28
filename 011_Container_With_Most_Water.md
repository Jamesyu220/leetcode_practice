You are given an integer array height of length n.  
There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).  
Find two lines that together with the x-axis form a container, such that the container contains the most water.  
Return the maximum amount of water a container can store.  

Example 1:  
```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```

Example 2:  
```
Input: height = [1,1]
Output: 1
```

Code:  
C++:  
```c++
class Solution {
public:
    int maxArea(vector<int>& height) {
        int start = 0, end = height.size() - 1;
        int area = 0;
        int h;
        while(start < end) {
            if(height[start] > height[end]) {
                h = height[end];
                if(h * (end - start) > area) area = h * (end - start);
                while(height[end] <= h && end > start) end--;
            }
            else if(height[start] < height[end]) {
                h = height[start];
                if(h * (end - start) > area) area = h * (end - start);
                while(height[start] <= h && end > start) start++;
            }
            else {
                h = height[start];
                if(h * (end - start) > area) area = h * (end - start);
                bool changed = false;
                for(int i = 1; i <= (end - start) / 2; ++i) {
                    if(height[start + i] > h && height[start + i] >= height[end - i]) {
                       start += i;
                       changed = true;
                       break;
                    }
                    else if(height[end - i] > h && height[start + i] <= height[end - i]) {
                        end -= i;
                        changed = true;
                        break;
                    }
                }
                if(!changed) break;
            }
        }
        return area;
    }
};
```

Runtime: 73 ms, faster than 99.69% of C++ online submissions.  
Memory Usage: 59 MB, less than 23.33% of C++ online submissions.  

Python:  
```python
class Solution(object):
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        front = 0
        back = len(height) - 1
        
        maxArea = 0
        while(True):
            maxArea = max(min(height[front], height[back]) * (back - front), maxArea)
            update = False
            
            if height[front] < height[back]:
                for i in range(front + 1, back):
                    if height[i] > height[front]: 
                        front = i
                        update = True
                        break
            elif height[front] > height[back]:
                for i in range(back - 1, front, -1):
                    if height[i] > height[back]: 
                        back = i
                        update = True
                        break
            else:
                for i in range(1, (back - front)/2 + 1):
                    if height[front+i] > height[front] and height[front+i] >= height[back-i]:
                        front += i
                        update = True
                        break
                    elif height[back-i] > height[back] and height[back-i] > height[front+i]:
                        back -= i
                        update = True
                        break

            
            if not update:
                break

        return maxArea            
```

Runtime: 1278 ms, faster than 5.2% of Python online submissions.  
Memory Usage: 23.8 MB, less than 80.22% of Python online submissions.  
