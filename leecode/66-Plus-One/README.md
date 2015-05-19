## 66	Plus One

Given a non-negative number represented as an array of digits, plus one to the number.

The digits are stored such that the most significant digit is at the head of the list.

## Solution

```C++
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        vector<int> ret;
        int carry = 0;
        for(int i=digits.size() -1; i>=0; i--){
        	int sum = 0;
        	if(i == digits.size() - 1)
        		sum = digits[i] + 1 + carry;
        	else
        		sum = digits[i] + carry;
        	carry = sum / 10;
        	ret.push_back(sum % 10);
    	}
    	if(carry>0) ret.push_back(carry);
    	reverse(ret.begin(), ret.end());
    	return ret;
    }
};
```