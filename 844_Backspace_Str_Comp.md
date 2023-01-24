Given two strings s and t, return true if they are equal when both are typed into empty text editors. '#' means a backspace character.  

Note that after backspacing an empty text, the text will continue empty.  
Example 1:  
```
Input: s = "ab#c", t = "ad#c"
Output: true
Explanation: Both s and t become "ac".
```
Example 2:  
```
Input: s = "ab##", t = "c#d#"
Output: true
Explanation: Both s and t become "".
```
Example 3:  
```
Input: s = "a#c", t = "b"
Output: false
Explanation: s becomes "c" while t becomes "b".
```

Code:  
```c++
class Solution {
public:
    bool backspaceCompare(string s, string t) {
        int i = 0;
        while(i < s.size()) {
            if(s[i] == '#') {
                if(i > 0) {
                    s.erase(i-1, 2);
                    i --;
                }
                else s.erase(s.begin() + i);
            }
            else i ++;
        }
        i = 0;
        while(i < t.size()) {
            if(t[i] == '#') {
                if(i > 0) {
                    t.erase(i-1, 2);
                    i --;
                }
                else t.erase(t.begin() + i);
            }
            else i ++;
        }
        if(s.size() != t.size()) return false;
        for(i = 0; i < s.size(); i++) {
            if(s[i] != t[i]) return false;
        }
        return true;
    }
};
```
Runtime: 2 ms, faster than 56.74% of C++ online submissions for backspace string compare.
Memory Usage: 6.3 MB, less than 47.51% of C++ online submissions for backspace string compare.
