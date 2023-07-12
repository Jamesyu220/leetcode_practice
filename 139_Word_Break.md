Given a string s and a dictionary of strings wordDict, return true if s can be segmented into a space-separated sequence of one or more dictionary words.  
Note that the same word in the dictionary may be reused multiple times in the segmentation.  

Example 1:  
```
Input: s = "leetcode", wordDict = ["leet","code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
```

Example 2:  
```
Input: s = "applepenapple", wordDict = ["apple","pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
Note that you are allowed to reuse a dictionary word.
```

Example 3:  
```
Input: s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]
Output: false
```

Code:  
```c++
// using dynamic programming
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        str = s;
        canBeBroken.resize(str.size(), 2);
        sort(wordDict.begin(), wordDict.end());
        return subWordBreak(wordDict, 0);
    }
    bool subWordBreak(vector<string>& wordDict, int i) {
        if(i == str.size()) return true;
        else if(i > str.size()) return false;
        if(canBeBroken[i] <= 1) return canBeBroken[i];

        // using binary search to find proper range [front, back) such that for all word:wordDict[front, back), word has same initial char with str[i:). 
        int front = 0, back = wordDict.size();
        if(wordDict[front][0] > str[i] || wordDict[back-1][0] < str[i]) {
            canBeBroken[i] = 0;
            return false; 
        }
        while(front < back - 1) {
            if(wordDict[front][0]==str[i] 
            && wordDict[back-1][0]==str[i]) break;
            int middle = (front + back) / 2;
            if(wordDict[middle][0] > str[i]) back = middle;
            else if(wordDict[middle][0] < str[i]) front = middle;
            else {
                if(wordDict[front][0] < str[i]) front ++;
                if(wordDict[back-1][0] > str[i]) back --;
            }
        }
        if(wordDict[front][0] != str[i]) {
            canBeBroken[i] = 0;
            return false;
        }
        for(int j = front; j < back; ++j) {
            if(str.substr(i, wordDict[j].size()) == wordDict[j] 
            && subWordBreak(wordDict, i + wordDict[j].size())) {
                canBeBroken[i] = 1;
                return true;
            }
        }
        canBeBroken[i] = 0;
        return false;
    }
private:
    string str;
    // 0: cannot be broken; 1: can be broken; 2: not visited
    vector<int> canBeBroken;
};
```

Runtime: 3 ms, faster than 99.22% of C++ online submissions.  
Memory Usage: 7.8 MB, less than 83.47% of C++ online submissions.
