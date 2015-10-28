## 66	Plus One

Given a non-negative number represented as an array of digits, plus one to the number.

The digits are stored such that the most significant digit is at the head of the list.

## Solution

```C++
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        vector<int> ret;
        const int n = digits.size() - 1;
        int carry = 0, sum = 0, val;
        for(int i=n; i>=0; i--){
        	if(i == n){
        		sum = digits[i] + 1;
        	}else{
        		sum = digits[i] + carry;
        	}
        	ret.push_back(sum % 10);
        	carry = sum / 10;
    	}
    	if(carry > 0) ret.push_back(carry);
    	reverse(ret.begin(), ret.end());
    	return ret;
    }
};
```