You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.  

Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.  

You may assume that you have an infinite number of each kind of coin.  
 
Example 1:  
```
Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1
```
Example 2:  
```
Input: coins = [2], amount = 3
Output: -1
```
Example 3:  
```
Input: coins = [1], amount = 0
Output: 0
```
 
Code:  
```c++
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        if(amount == 0) return 0;
        sort(coins.begin(), coins.end());
        num.resize(amount + 1);
        for(int i = 1; i <= amount; ++i) {
            if(i < coins[0]) {
                num[i] = -1;
                continue;
            }
            int min = 100000;
            for(int j = 0; j < coins.size() && coins[j] <= i; ++j) {
                if(num[i-coins[j]] >= 0 && num[i-coins[j]] < min) min = num[i-coins[j]];
            }
            if(min == 100000) num[i] = -1;
            else num[i] = min + 1;
        }
        return num[amount];
    }
    vector<int> num;
};
 ```
Runtime: 107 ms, faster than 57.23% of C++ online submissions.  
Memory Usage: 14.6 MB, less than 62.34% of C++ online submissions.
