## 172	Factorial Trailing Zeroes

Given an integer n, return the number of trailing zeroes in n!.

Note: Your solution should be in logarithmic time complexity.

## Solution
遍历并计算5的个数的算法会超时。可以看到规律
5！=> 1 => 5/5
10! => 2 => 10/5
15! => 3 => 15/5
25! => 6 => 25/5 + 5/5
```C++
class Solution {
public:
    int trailingZeroes(int n) {
        int ret = 0;
        while(n){
            ret += n / 5;
            n /= 5;
        }
        return ret;
    }
};
```