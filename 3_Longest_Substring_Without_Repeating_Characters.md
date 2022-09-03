Problem:  
Given a string s, find the length of the longest substring without repeating characters.  
```python
class Solution(object):
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        if(len(s) == 0): return 0
        index = {}
        maxsubstrlen = 0
        start = 0 
    
        for i in range(len(s)):
            if s[i] not in index:
                if i == len(s) - 1 and i - start + 1 > maxsubstrlen:
                    maxsubstrlen = i - start + 1
            elif index[s[i]] < start:
                if i == len(s) - 1 and i - start + 1 > maxsubstrlen:
                    maxsubstrlen = i - start + 1
            else:
                if i - start > maxsubstrlen:
                    maxsubstrlen = i - start
                start = index[s[i]] + 1
            index[s[i]] = i           
        return maxsubstrlen
```
Runtime: 47 ms, faster than 90.46% of Python online submissions for Longest Substring Without Repeating Characters.  
Memory Usage: 14.3 MB, less than 30.18% of Python online submissions for Longest Substring Without Repeating Characters.  
