Given a string s which consists of lowercase or uppercase letters, return the length of the longest palindrome that can be built with those letters.  

Letters are case sensitive, for example, "Aa" is not considered a palindrome here.  

Code:  
```c
class Solution {
public:
    int longestPalindrome(string s) {
        vector<int> frequency(52, 0);
        for(int i = 0; i < s.size(); ++i) {
            if(s[i] <= 'Z') frequency[s[i] - 'A'] ++;
            else frequency[26 + s[i] - 'a'] ++;
        }
        bool odd_exist = false;
        int pal_len = 0;
        for(int i = 0; i < 52; ++i) {
            if(frequency[i] % 2 == 1) {
                pal_len += frequency[i] - 1;
                odd_exist = true;
            }
            else pal_len += frequency[i];
        }
        if(odd_exist) pal_len ++;
        return pal_len;
    }
};
```
Runtime: 7 ms, faster than 42.69% of C++ online submissions for Longest Palindrome.  
Memory Usage: 6.7 MB, less than 49.22% of C++ online submissions for Longest Palindrome.  
