## 242 VAlid Anagram

Given two strings s and t, write a function to determine if t is an anagram of s.

For example,
s = "anagram", t = "nagaram", return true.
s = "rat", t = "car", return false.

Note:
You may assume the string contains only lowercase alphabets.

## Solution

```C++
class Solution {
public:
    bool isAnagram(string s, string t) {
        int buf[256] = {0};
        for(int i=0; i<s.size(); i++){
            buf[s[i]] +=1;
        }
        for(int i=0; i<t.size(); i++){
            buf[t[i]] -= 1;
        }
        for(int i=0; i<256; i++){
            if(buf[i] != 0)
                return false;
        }
        return true;
    }
};
```

