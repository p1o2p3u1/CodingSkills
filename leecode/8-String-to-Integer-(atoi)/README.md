## 8	String to Integer (atoi)

Implement atoi to convert a string to an integer.

Hint: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

## Solution
```C++
class Solution {
private:
    bool isNumeric(char c){
        if(c >='0' && c <='9') return true;
        else return false;
    }
    bool isWhiteSpace(char c){
        if(c == ' ' || c == '\t' || c == '\n') return true;
        else return false;
    }
public:
    int myAtoi(string str) {
        int i = 0;
        int sign = 1;
        while(i < str.length() && isWhiteSpace(str[i])) i++;
        if(str[i] == '+') i++;
        else if(str[i] == '-') {sign = -1;i++;}
        long ret = 0;
        while(i < str.length()){
            if(isNumeric(str[i])){
                ret = ret * 10 + str[i] - '0';
                i++;
                if(sign == 1 && ret > 2147483647) return INT_MAX;
                if(sign == -1 && ret > 2147483648) return INT_MIN; 
            }else break;
        }
        return sign * ret;
    }
};

```