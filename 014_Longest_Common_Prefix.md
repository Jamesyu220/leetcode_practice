Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string ```""```.  

Example 1:  
```
Input: strs = ["flower","flow","flight"]
Output: "fl"
```

Example 2:  
```
Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

Code:  
```c++
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        string common_prefix = "";
        bool common;
        for(int i = 0; i < strs[0].size(); ++i) {
            common = true;
            for(int j = 1; j < strs.size(); ++j) {
                if(strs[j].size() <= i || strs[j][i] != strs[0][i]) {
                    common = false;
                    break;
                }
            }
            if(common) common_prefix += strs[0][i];
            else return common_prefix;
        }
        return common_prefix;
    }
};
```
Runtime: 3 ms, faster than 91.4% of C++ online submissions for Longest Common Prefix.  
Memory Usage: 9.2 MB, less than 53.39% of C++ online submissions for Longest Common Prefix.  
