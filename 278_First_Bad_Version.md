You are a product manager and currently leading a team to develop a new product.  
Unfortunately, the latest version of your product fails the quality check.  
Since each version is developed based on the previous version, all the versions after a bad version are also bad.  

Suppose you have n versions [1, 2, ..., n] and you want to find out the first bad one, which causes all the following ones to be bad.  

You are given an API bool isBadVersion(version) which returns whether version is bad.  
Implement a function to find the first bad version. You should minimize the number of calls to the API.  

Code:  
```c
// The API isBadVersion is defined for you.
// bool isBadVersion(int version);

class Solution {
public:
    int firstBadVersion(int n) {
        unsigned int front = 1;
        unsigned int back = n;
        unsigned int middle;
        if(isBadVersion(1)) return 1;
        while(true) {
            middle = (front + back) / 2;
            if(isBadVersion(middle)) {
                if(middle < front + 2) return middle;
                back = middle;
            }                
            else {
                if(middle > back - 2) return back;
                front = middle;
            }   
        }
    }
};
```
Runtime: 0 ms, faster than 100.00% of C++ online submissions for First Bad Version.  
Memory Usage: 5.9 MB, less than 67.72% of C++ online submissions for First Bad Version.
