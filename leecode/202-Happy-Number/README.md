# 202	Happy Number

Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

Example: 19 is a happy number
```
1*1 + 9*9 = 82
8*8 + 2*2 = 68
6*6 + 8*8 = 100
1*1 + 0*0 + 0*0 = 1
```

# Solution
用一个map来记录出现过的数，防止出现死循环。
```C++
class Solution {
private: 
    int next(int n){
        int ret = 0;
        while(n){
            int d = n % 10;
            n /= 10;
            ret += d * d;
        }
        return ret;
    }
    bool isHappy(int n, unordered_map<int, bool> &m){
        if(n == 1) return true;
        if(m[n]) return false;
        m[n] = true;
        return isHappy(next(n), m);
    }
public:
    bool isHappy(int n) {
        if(n == 1) return true;
        unordered_map<int, bool> m;
        m[n] = true;
        return isHappy(next(n), m);
    }
};
```
