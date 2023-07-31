Given an integer ```x```, return true if ```x``` is a palindrome, and false otherwise.  

Example 1:  
```
Input: x = 121
Output: true
Explanation: 121 reads as 121 from left to right and from right to left.
```

Example 2:  
```
Input: x = -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```

Example 3:  
```
Input: x = 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

Code:  
Python:  
```python
class Solution(object):
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        if x < 0:
            return False
        if x < 10:
            return True
        
        s = str(x)
        L = len(s)
        for i in range(0, L/2):
            if s[i] != s[L-1-i]:
                return False
        
        return True
```

Runtime: 38 ms, faster than 96.47% of Python online submissions.  
Memory Usage: 13.3 MB, less than 62.11% of Python online submissions.
