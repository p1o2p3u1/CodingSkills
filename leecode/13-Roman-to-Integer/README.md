## 13	Roman to Integer

Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.

## Solution
```C++
class Solution {
public:
    int romanToInt(string s) {
        if(s.length() == 0) return 0;
        unordered_map<char, int> m;
        m['I'] = 1;
        m['V'] = 5;
        m['X'] = 10;
        m['L'] = 50;
        m['C'] = 100;
        m['D'] = 500;
        m['M'] = 1000;
        const int n = s.length() - 1;
        int ret = m[s[n]];
        int pre = m[s[n]];
        for(int i=n-1; i>=0; i--){
        	int v = m[s[i]];
        	if(v < pre) ret -= v;
        	else ret += v;
        	pre = v;
    	}
    	return ret;
    }
};
```