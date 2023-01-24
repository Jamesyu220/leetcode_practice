Given an integer n, return an array ans of length n + 1 such that for each i (0 <= i <= n), ans[i] is the number of 1's in the binary representation of i.  

Example 1:  
```
Input: n = 2
Output: [0,1,1]
Explanation:
0 --> 0
1 --> 1
2 --> 10
```
Example 2:  
```
Input: n = 5
Output: [0,1,1,2,1,2]
Explanation:
0 --> 0
1 --> 1
2 --> 10
3 --> 11
4 --> 100
5 --> 101
```

Code:  
```c++
class Solution {
public:
    vector<int> countBits(int n) {
        vector<int> ans(n + 1);
        ans[0] = 0;
        int base = 1, remainder = 0;
        for(int i = 1; i <= n; ++i) {
            if(remainder < base/2)  ans[i] = ans[base/2 + remainder];
            else                    ans[i] = ans[remainder] + 1;

            if(remainder < base - 1) remainder ++;
            else {
                remainder = 0;
                base *= 2;
            }                 
        }
        return ans;
    }
};
```
Runtime: 6 ms, faster than 72.4% of C++ online submissions for Roman to Integer.  
Memory Usage: 8 MB, less than 51.93% of C++ online submissions for Roman to Integer.  
