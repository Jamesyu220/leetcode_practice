Implement the myAtoi(string s) function, which converts a string to a 32-bit signed integer (similar to C/C++'s atoi function).  

The algorithm for myAtoi(string s) is as follows:  
1. Read in and ignore any leading whitespace.  
2. Check if the next character (if not already at the end of the string) is '-' or '+'. Read this character in if it is either.
This determines if the final result is negative or positive respectively. Assume the result is positive if neither is present.
3. Read in next the characters until the next non-digit character or the end of the input is reached. The rest of the string is ignored.  
4. Convert these digits into an integer (i.e. "123" -> 123, "0032" -> 32). If no digits were read, then the integer is 0. Change the sign as necessary (from step 2).  
5. If the integer is out of the 32-bit signed integer range [-2^31, 2^31 - 1], then clamp the integer so that it remains in the range. Specifically, integers less than -2^31 should be clamped to -2^31, and integers greater than 2^31 - 1 should be clamped to 2^31 - 1.  
6. Return the integer as the final result.  

Note:  
Only the space character ' ' is considered a whitespace character.  
Do not ignore any characters other than the leading whitespace or the rest of the string after the digits.  

Example 1:  
```
Input: s = "42"
Output: 42
Explanation: The underlined characters are what is read in, the caret is the current reader position.
Step 1: "42" (no characters read because there is no leading whitespace)
         ^
Step 2: "42" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "42" ("42" is read in)
           ^
The parsed integer is 42.
Since 42 is in the range [-231, 231 - 1], the final result is 42.
```

Example 2:  
```
Input: s = "   -42"
Output: -42
Explanation:
Step 1: "   -42" (leading whitespace is read and ignored)
            ^
Step 2: "   -42" ('-' is read, so the result should be negative)
             ^
Step 3: "   -42" ("42" is read in)
               ^
The parsed integer is -42.
Since -42 is in the range [-231, 231 - 1], the final result is -42.
```

Example 3:  
```
Input: s = "4193 with words"
Output: 4193
Explanation:
Step 1: "4193 with words" (no characters read because there is no leading whitespace)
         ^
Step 2: "4193 with words" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "4193 with words" ("4193" is read in; reading stops because the next character is a non-digit)
             ^
The parsed integer is 4193.
Since 4193 is in the range [-231, 231 - 1], the final result is 4193.
```

Code:  
```c++
class Solution {
public:
    int myAtoi(string s) {
        int i = 0;
        while(i < s.size() && s[i] == ' ') ++i;
        s = s.substr(i);

        if(s.empty()) return 0;
        int prefix = 1;
        if(s[0] == '-') {
            prefix = -1;
            s = s.substr(1);
        } 
        else if(s[0] == '+') s = s.substr(1);

        i = 0;
        int num = 0;
        while(i < s.size() && s[i] >= '0' && s[i] <= '9') {
            if(prefix > 0) {
                if(num<=(2147483647-(s[i]-'0'))/10) num = num*10+(s[i]-'0');
                else {
                    num = 2147483647;
                    return num;
                }
            } 
            else {
                if(num>=(-2147483648+(s[i]-'0'))/10) num=num*10-(s[i]-'0');
                else {
                    num = -2147483648;
                    return num;
                }
            } 

            ++i;
        }
        
        return num;
    }
};
```

Runtime: 3 ms, faster than 73.86% of C++ online submissions.  
Memory Usage: 7 MB, less than 47.85% of C++ online submissions.
