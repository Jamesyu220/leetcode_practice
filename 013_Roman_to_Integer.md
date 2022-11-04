Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.  
```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```
Given a roman numeral, convert it to an integer.  

Example 1:  
```
Input: s = "III"
Output: 3
Explanation: III = 3.
```
Example 2:  
```
Input: s = "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
```
Example 3:  
```
Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

Code:  
```c++
class Solution {
public:
    int romanToInt(string s) {
        int sum = 0;
        for(int i = 0; i < s.size(); ++i) {
            if(s[i] == 'M') sum += 1000;
            else if(s[i] == 'D') sum += 500;
            else if(s[i] == 'C') {
                if(s[i+1] == 'D' || s[i+1] == 'M') sum -= 100;
                else sum += 100;
            }
            else if(s[i] == 'L') sum += 50;
            else if(s[i] == 'X') {
                if(s[i+1] == 'L' || s[i+1] == 'C') sum -= 10;
                else sum += 10;
            }
            else if(s[i] == 'V') sum += 5;
            else if(s[i+1] == 'V' || s[i+1] == 'X') sum -= 1;
            else sum += 1;   
        }
        return sum;
    }
};
```
Runtime: 3 ms, faster than 98.95% of C++ online submissions for Roman to Integer.  
Memory Usage: 6 MB, less than 66.09% of C++ online submissions for Roman to Integer.  
