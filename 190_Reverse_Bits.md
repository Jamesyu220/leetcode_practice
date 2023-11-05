Reverse bits of a given 32 bits unsigned integer.  

Note:  
Note that in some languages, such as Java, there is no unsigned integer type. In this case, both input and output will be given as a signed integer type.  
They should not affect your implementation, as the integer's internal binary representation is the same, whether it is signed or unsigned.  
In Java, the compiler represents the signed integers using 2's complement notation. Therefore, in Example 2 above, the input represents  
the signed integer -3 and the output represents the signed integer -1073741825.  

Example 1:  
```
Input: n = 00000010100101000001111010011100
Output:    964176192 (00111001011110000010100101000000)
Explanation: The input binary string 00000010100101000001111010011100 represents the unsigned integer 43261596, so return 964176192 which its binary representation is 00111001011110000010100101000000.
```

Example 2:  
```
Input: n = 11111111111111111111111111111101
Output:   3221225471 (10111111111111111111111111111111)
Explanation: The input binary string 11111111111111111111111111111101 represents the unsigned integer 4294967293, so return 3221225471 which its binary representation is 10111111111111111111111111111111.
```

Code:  
```c++
class Solution {
public:
    uint32_t reverseBits(uint32_t n) {
        bitset<32> bs(n), bsr;
        for(int i = 0; i < 32; ++i) bsr[i] = bs[31-i];
        uint32_t r = (uint32_t) bsr.to_ulong();
        return r;
    }
};
```

Runtime: 0 ms, faster than 100% of C++ online submissions.  
Memory Usage: 6.25 MB, less than 80.2% of C++ online submissions.  
