Given two binary strings a and b, return their sum as a binary string.  

```
Example 1:
Input: a = "11", b = "1"
Output: "100"
```

```
Example 2:
Input: a = "1010", b = "1011"
Output: "10101"
```
Code:  
```c++
class Solution {
public:
    string addBinary(string a, string b) {
        string longer = (a.size() >= b.size())? a: b;
        string shorter = (a.size() < b.size())? a: b;
        string sum = "";
        bool c = false, s = false;
        int diff = longer.size() - shorter.size();
        for(int i = shorter.size() - 1; i >= 0; --i) {
            int ln = longer[i+diff] - '0', sh = shorter[i] - '0';
            s = (ln ^ sh) ^ c;
            c = (ln && sh) || (sh && c) || (ln && c);
            if(s) sum = '1' + sum;
            else sum = '0' + sum;
        }
        for(int i = diff - 1; i >= 0; --i) {
            int ln = longer[i] - '0';
            s = ln ^ c;
            c = ln && c;
            if(s) sum = '1' + sum;
            else sum = '0' + sum;
        }
        if(c) sum = '1' + sum;
        return sum;
    }
};
```

Runtime: 7 ms, faster than 43.51% of C++ online submissions for Add Binary.  
Memory Usage: 7.1 MB, less than 7.33% of C++ online submissions for Add Binary.  
