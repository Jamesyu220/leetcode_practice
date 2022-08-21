Problem:  
A phrase is a palindrome if, after converting all uppercase letters into  
lowercase letters and removing all non-alphanumeric characters, it reads  
the same forward and backward. Alphanumeric characters include letters   
and numbers.

Given a string s, return true if it is a palindrome, or false otherwise.  

code:  
Python:  
```python
class Solution(object):
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        temp = []
        for charac in s:
            asc = ord(charac)
            if asc >= 65 and asc <= 90:
                temp.append(asc + 32)
            elif (asc >= 97 and asc <= 122) or (asc >= 48 and asc <= 57):
                temp.append(asc)
        if len(temp) == 0:
            return True
        for i in range(len(temp)/2 + 1):
            if temp[i] != temp[len(temp) - 1 - i]:
                return False
        return True
```
