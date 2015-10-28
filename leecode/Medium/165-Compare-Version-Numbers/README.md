## 165	Compare Version Numbers	

Compare two version numbers version1 and version2.
If version1 > version2 return 1, if version1 < version2 return -1, otherwise return 0.

You may assume that the version strings are non-empty and contain only digits and the . character.
The . character does not represent a decimal point and is used to separate number sequences.
For instance, 2.5 is not "two and a half" or "half way to version three", it is the fifth second-level revision of the second first-level revision.

Here is an example of version numbers ordering:
```
0.1 < 1.1 < 1.2 < 13.37
```

## Solution
坑有点多，比如如下几个
```C++
/*
01 0 return 0
1.0 1 return 0
1.0.0.0.0 1 return 0
*/
class Solution {
private:
    bool dotZeros(string s, int i){
        while(i < s.length()){
            if(s[i] == '.' || s[i] == '0') 
                i++;
            else
                return false;
        }
        return true;
    }
public:
    int compareVersion(string version1, string version2) {
        int i=0,j=0;
        while(i < version1.length() && j < version2.length()){
            // 01 1
            int v1 = 0,v2 = 0;
            while(i < version1.length() && version1[i] != '.') v1 = v1 * 10 + version1[i++] - '0';
            while(j < version2.length() && version2[j] != '.') v2 = v2 * 10 + version2[j++] - '0';
            if(v1 > v2) return 1;
            else if(v1 < v2) return -1;
            else {
                if(i < version1.length() && j < version2.length()){
                    i++; j++;
                }else
                    break;
            } 
        }
        // 1 1.0.0.0.0
        // 1.2 1.2.3
        if(i == version1.length() && j < version2.length() && !dotZeros(version2, j)) return -1;
        // 1.2.3 1.2
        // 1.0.0.0 1
        if(i < version1.length() && j == version2.length() && !dotZeros(version1, i)) return 1;
        // 1.2.3 1.2.3
        return 0;
    }
};
```