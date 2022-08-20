code  
c++:  
```c
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

python:  
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
