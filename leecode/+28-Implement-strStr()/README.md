## 28	Implement strStr()

Implement strStr().

Returns the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

## Solution
O(mn)
```C++
class Solution {
public:
    int strStr(string haystack, string needle) {
    	if(haystack.length() < needle.length()) return -1;
        for(int i=0; i<haystack.length() - needle.length() + 1; i++){
        	int j;
        	for(j=0; j<needle.length(); j++){
        		if(haystack[i + j] != needle[j])
        			break;
        	}
        	if(j == needle.length()) return i;
    	}
    	return -1;
    }
};
```

O(m+n)
```C++

```