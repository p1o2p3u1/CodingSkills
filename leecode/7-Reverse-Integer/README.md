## 7	Reverse Integer	

Reverse digits of an integer.

Example1: x = 123, return 321
Example2: x = -123, return -321

## Solution

将和定义为long型就可以了。
```C++
class Solution {
public:
    int reverse(int x) {
        long ret = 0;
        while(x){
            ret = ret * 10 + x % 10;
            x /= 10;
        }
        if(ret > INT_MAX || ret < INT_MIN) return 0;
        return ret;
    }
};
```