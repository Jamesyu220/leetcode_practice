Given a string ```s``` containing just the characters ```'('```, ```')'```, ```'{'```, ```'}'```, ```'['``` and ```']'```, determine if the input string is valid.  

An input string is valid if:  
1.Open brackets must be closed by the same type of brackets.  
2.Open brackets must be closed in the correct order.  
3.Every close bracket has a corresponding open bracket of the same type.  
 
Example 1:  
```
Input: s = "()"
Output: true
```

Example 2:  
```
Input: s = "()[]{}"
Output: true
```

Example 3:  
```
Input: s = "(]"
Output: false
```

Code:  
C++:  
```c++
class Solution {
public:
    bool isValid(string s) {
        vector<char> stack;
        for(int i = 0; i < s.length(); ++i) {
            if(s[i] == ')') {
                if(stack.empty()) return false;
                if(stack.back() == '(') stack.pop_back();
                else return false;
            }
            else if(s[i] == ']') {
                if(stack.empty()) return false;
                if(stack.back() == '[') stack.pop_back();
                else return false;
            }
            else if(s[i] == '}') {
                if(stack.empty()) return false;
                if(stack.back() == '{') stack.pop_back();
                else return false;
            }
            else stack.push_back(s[i]);
        }
        cout << "hello" << endl;
        if(stack.empty()) return true;
        else return false;
    }
};
```

Runtime: 0ms, beats 100% of users with C++.  
Memory: 6.3mb, beats 35.62% of users with C++.  

Python:  
```python
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = []
        for i in range(len(s)):
            if s[i] == ')':
                if len(stack) == 0:
                    return False
                if stack[-1] == '(':
                    stack.pop()
                else:
                    return False
            elif s[i] == ']':
                if len(stack) == 0:
                    return False
                if stack[-1] == '[':
                    stack.pop()
                else:
                    return False
            elif s[i] == '}':
                if len(stack) == 0:
                    return False
                if stack[-1] == '{':
                    stack.pop()
                else:
                    return False
            else:
                stack.append(s[i])
        if len(stack) == 0:
            return True
        else:
            return False
```

Runtime: 13ms, beats 86.85% of users with Python.  
Memory: 13.6mb, beats 23.89% of users with Python.  
