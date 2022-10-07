Given two strings ransomNote and magazine, return true if ransomNote can be constructed by using the letters from magazine and false otherwise.  

Each letter in magazine can only be used once in ransomNote.  

Code:  
```c
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        if(ransomNote.size() > magazine.size()) return false;
        vector<int> frequency;
        frequency.resize(26);
        for(int i = 0; i < 26; ++i) frequency[i] = 0;
        for(int i = 0; i < magazine.size(); ++i) frequency[magazine[i] - 'a'] ++;
        for(int i = 0; i < ransomNote.size(); ++i) {
            if(!frequency[ransomNote[i] - 'a']--) return false;
        }
        return true;
    }
};
```
Runtime: 48 ms, faster than 15.61% of C++ online submissions for Ransom Note.  
Memory Usage: 8.8 MB, less than 40.20% of C++ online submissions for Ransom Note.  
