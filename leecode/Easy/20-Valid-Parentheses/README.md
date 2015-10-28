## 20	Valid Parentheses

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

## Solution

```C++
class Solution {
public:
    bool isValid(string str) {
    	stack<char> s;
    	unordered_map<char, char> m = {
    		{')', '('},
    		{']', '['},
    		{'}', '{'}
    	};
    	for(int i=0; i<str.length(); i++){
    		char c = str[i];
    		if(c == '(' || c == '[' || c =='{') 
    			s.push(c);
    		else{
    			if(!s.empty() && m[c] == s.top()) s.pop();
    			else return false;
    		}
    	}
    	if(s.empty()) return true;
    	else return false;    
    }
};
```