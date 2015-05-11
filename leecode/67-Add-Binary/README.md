## 67	Add Binary
Given two binary strings, return their sum (also a binary string).

For example,
```
a = "11"
b = "1"
Return "100".
```

## Solution

```C++
class Solution {
public:
    string addBinary(string a, string b) {
        int i = a.length() - 1;
        int j = b.length() - 1;
        int carry = 0;
        string ret;
        while(i >=0 && j >=0){
        	int sum = a[i] - '0' + b[j] - '0' + carry;
        	ret += sum % 2 + '0';
        	carry = sum / 2;
    	}
    	while(i >= 0){
    		
    	}
    	while(j >= 0){

    	}
    }
};
```