Given an array of distinct integers candidates and a target integer target, return a list of all unique combinations of candidates where the chosen numbers sum to target.  
You may return the combinations in any order.

The same number may be chosen from candidates an unlimited number of times.  
Two combinations are unique if the frequency of at least one of the chosen numbers is different.  

The test cases are generated such that the number of unique combinations that sum up to target is less than 150 combinations for the given input.  

Example 1:  
```
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.
```

Example 2:  
```
Input: candidates = [2,3,5], target = 8
Output: [[2,2,2,2],[2,3,3],[3,5]]
```

Example 3:  
```
Input: candidates = [2], target = 1
Output: []
```

Code:  
```c++
class Solution {
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<vector<int>> combinations, subCombinations;
        for(int i = 0; i < candidates.size(); ++i) {
            subCombinations = findCombinations({candidates[i]}, i, candidates, target);
            combinations.insert(combinations.end(), subCombinations.begin(), subCombinations.end());
        }
        return combinations;
    }
    vector<vector<int>> findCombinations(vector<int> combination, int index, vector<int>& candidates, int target) {
        int sum = 0;
        vector<vector<int>> combinations;
        for(int i = 0; i < combination.size(); ++i) sum += combination[i];
        if(sum == target) combinations.push_back(combination);
        if(sum >= target) return combinations; 
        vector<vector<int>> subCombinations;
        for(int i = index; i < candidates.size(); ++i) {
            combination.push_back(candidates[i]);
            subCombinations = findCombinations(combination, i, candidates, target);
            combinations.insert(combinations.end(), subCombinations.begin(), subCombinations.end());
            combination.pop_back();
        }
        return combinations;
    }
};
```

Runtime: 40 ms, faster than 25.12% of C++ online submissions.  
Memory Usage: 17.3 MB, less than 28.7% of C++ online submissions.
