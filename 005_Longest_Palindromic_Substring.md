Given a string ```s```, return the longest palindromic substring in ```s```.

Example 1:  
```
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.
```

Example 2:  
```
Input: s = "cbbd"
Output: "bb"
```

Code:  
C++:  
```c++
class Solution {
public:
    string longestPalindrome(string s) {
        if(s.size() == 1) return s;
        int start, end;
        int max = 0;
        for(int i = 1; i < s.size()-1; ++i) {
            int k;
            for(k = 0; k < i && k < s.size() - i; ++k) {
                if(s[i-1-k] != s[i+k]) break;
            }
            if(2*k > max) {
                max = 2*k;
                start = i-k;
                end = i+k-1;
            }
            for(k = 0; k < i && k < s.size() - i - 1; ++k) {
                if(s[i-1-k] != s[i+1+k]) break;
            }
            if(2*k+1 > max) {
                max = 2*k+1;
                start = i-k;
                end = i+k;
            }
        }
        if(max < 2) {
            if(s[s.size()-2] == s[s.size()-1]) return s.substr(s.size()-2, 2);
            else return s.substr(0, 1);
        }
        return s.substr(start, end - start + 1);
    }
};
```

Runtime: 21 ms, faster than 76.26% of C++ online submissions.  
Memory Usage: 6.8 MB, less than 86.59% of C++ online submissions.  

Python:  
```python
class Solution(object):
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        if len(s) == 1:
            return s
        
        if s[0] == s[1]:
            start = 0
            end = 2
        else:
            start = 0
            end = 1
        maxlen = end - start
        
        for i in range(2, len(s)):
            if s[i] == s[i-2]:
                center = i-1
                r = 1
                while True:
                    if center-r >= 1 and center+r <= len(s)-2:
                        if s[center-r-1] == s[center+r+1]:
                            r += 1
                        else:
                            break
                    else:
                        break
                
                if 2*r+1 > maxlen:
                    start = center - r
                    end = center + r + 1
                    maxlen = end - start
                    
            if s[i] == s[i-1]:
                r = 0
                while True:
                    if i-1-r >= 1 and i+r <= len(s)-2:
                        if s[i-r-2] == s[i+r+1]:
                            r += 1
                        else:
                            break
                    else:
                        break
                    
                if 2*(r+1) > maxlen:
                    start = i-1-r
                    end = i+r+1
                    maxlen = end - start
        
        return s[start: end]
```

Runtime: 1332 ms, faster than 39.2% of Python online submissions.  
Memory Usage: 13.7 MB, less than 23.64% of Python online submissions.  
