Given two strings s and t, return true if t is an anagram of s, and false otherwise.  

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.  

Code:  
```python
class Solution(object):
    def isAnagram(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        numOfChar = {}
        for char in s:
            if char not in numOfChar:
                numOfChar[char] = 1
            else:
                numOfChar[char] += 1
        
        for char in t:
            if char not in numOfChar:
                return False
            if numOfChar[char] < 1:
                return False
            numOfChar[char] -= 1
        
        for item in numOfChar:
            if numOfChar[item] != 0:
                return False
        
        return True
```
Runtime: 42 ms, faster than 89.19% of Python online submissions for Valid Anagram.  
Memory Usage: 14 MB, less than 65.38% of Python online submissions for Valid Anagram.  
