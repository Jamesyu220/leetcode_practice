You are climbing a staircase. It takes n steps to reach the top.  

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?  

Code:  
```c
class Solution {
public:
    int climbStairs(int n) {
        // Fibonacci sequence: F(n) = F(n-1) + F(n-2), F(0) = 1, F(1) = 1
        int small = 1, large = 1;
        for(int i = 2; i <= n; ++i) {
            large += small;
            small = large - small;
        }
        return large;
    }
};
```

Runtime: 3 ms, faster than 36.07% of C++ online submissions for Climbing Stairs.  
Memory Usage: 6 MB, less than 56.99% of C++ online submissions for Climbing Stairs.  
