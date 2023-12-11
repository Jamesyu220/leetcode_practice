Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.  

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.  

Example 1:  
```
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

Example 2:  
```
Input: digits = ""
Output: []
```

Example 3:  
```
Input: digits = "2"
Output: ["a","b","c"]
```

Code:  
```c++
class Solution {
public:
    vector<string> letterCombinations(string digits) {
        if(!digits.size()) return {};
        vector<vector<char>> letters;
        letters.resize(digits.size());
        for(int i = 0; i < digits.size(); ++i) {
            switch(digits[i]) {
                case '2':
                    letters[i] = {'a', 'b', 'c'};
                    break;
                case '3':
                    letters[i] = {'d', 'e', 'f'};
                    break;
                case '4':
                    letters[i] = {'g', 'h', 'i'};
                    break;
                case '5':
                    letters[i] = {'j', 'k', 'l'};
                    break;
                case '6':
                    letters[i] = {'m', 'n', 'o'};
                    break;
                case '7':
                    letters[i] = {'p', 'q', 'r', 's'};
                    break;
                case '8':
                    letters[i] = {'t', 'u', 'v'};
                    break;
                case '9':
                    letters[i] = {'w', 'x', 'y', 'z'};
                    break;
            }

        }
        int num = 1;
        for(int i = 0; i < letters.size(); ++i) {
            num *= letters[i].size();
        }
        vector<string> combinations(num);
        for(int i = 0; i < letters.size(); ++i) {
            num /= letters[i].size();
            for(int j = 0; j < letters[i].size(); ++j) {
                for(int k = 0; k < combinations.size(); ++k) {
                    int mod = k % (num * letters[i].size());
                    if(mod >= num * j && mod < num * (j + 1)) combinations[k] += letters[i][j];
                }
            }
        }
        return combinations;
    }
};
```

Runtime: 0 ms, faster than 100% of C++ online submissions.  
Memory Usage: 7 MB, less than 48.37% of C++ online submissions.  
