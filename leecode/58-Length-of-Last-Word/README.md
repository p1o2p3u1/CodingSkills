## 58	Length of Last Word

Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

If the last word does not exist, return 0.

Note: A word is defined as a character sequence consists of non-space characters only.

For example, 
Given s = "Hello World",
return 5.

## Solution
判断边界条件，以及`a `这类的情况。
```C++
class Solution {
public:
    int lengthOfLastWord(string s) {
        if(s.length() == 0) return 0;
        int ret = 0;
        int n = s.length() - 1;
        while(s[n] == ' ') n--;
        while(n >= 0){
            if(s[n--] != ' ') ret++;
            else break;
        }
        return ret;
    }
};
```