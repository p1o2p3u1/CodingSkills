## 14	Longest Common Prefix

Write a function to find the longest common prefix string amongst an array of strings.

## Solution

```C++
/*
abcde
abccd
ab
ab
*/
class Solution {
public:
    string longestCommonPrefix(vector<string> &strs) {
        if(strs.size() == 0) return "";
        for(int i=0; i<strs[0].length(); i++){
        	for(int j=1; j<strs.size(); j++){
        		if(i == strs[j].length() || strs[j][i] != strs[0][i])
        			return strs[0].substr(0, i);
        	}	
    	}
    	return strs[0];
    }
};
```