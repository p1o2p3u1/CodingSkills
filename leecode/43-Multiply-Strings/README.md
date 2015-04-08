## 43	Multiply Strings
Given two numbers represented as strings, return multiplication of the numbers as a string.

Note: The numbers can be arbitrarily large and are non-negative.

## Solution 
纯模拟
```C++
class Solution {
private:
    string multiply(string num, char c){
        stringstream ss;
        int carry = 0;
        reverse(num.begin(), num.end());
        for(int i=0; i<num.length(); i++){
            int base = num[i] - '0';
            int sum = (c - '0') * base + carry;
            ss << sum % 10;
            carry = sum / 10;
        }
        if(carry!=0) ss<<carry;
        string ret = ss.str();
        reverse(ret.begin(), ret.end());
        return ret;
    }
    string add(string num1, string num2){
        stringstream ss;
        reverse(num1.begin(), num1.end());
        reverse(num2.begin(), num2.end());
        int carry = 0;
        int n = max(num1.length(), num2.length());
        for(int i=0; i<n; i++){
            int a = 0, b=0;
            if(i<num1.length()) a = num1[i] - '0';
            if(i<num2.length()) b = num2[i] - '0';
            int sum = a + b + carry;
            ss << sum % 10;
            carry = sum / 10;
        }
        if(carry !=0) ss<<carry;
        string ret = ss.str();
        reverse(ret.begin(), ret.end());
        return ret;
    }
    string shiftLeft(string num, int k){
        stringstream ss;
        ss << num;
        while(k--) ss << 0;
        return ss.str();
    }
public:
    string multiply(string num1, string num2) {
        int n = num2.length();
        string ret("0");
        if(num2 == "0" || num1 == "0") return ret;
        for(int i=n-1; i>=0; i--){
            string m = multiply(num1, num2[i]);
            m = shiftLeft(m, n-i-1);
            ret = add(m, ret);
        }
        return ret;
    }
};
```
