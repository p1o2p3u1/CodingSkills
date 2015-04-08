## 28	Implement strStr()
Implement strStr().

Returns the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

## Solution
有回溯的双重迭代版，时间复杂度O(mn)，比较容易实现。
```C++
class Solution {
public:
    int strStr(char *haystack, char *needle) {
        if(haystack == NULL || needle == NULL) return -1;
        int len1 = strlen(haystack);
        int len2 = strlen(needle);
        int i,j;
        if(len2 > len1) return -1;
        
        for(i=0; i<len1-len2+1; i++){ // 注意这个地方要有个+1
            for(j=0; j<len2; j++){
                if(haystack[i + j] != needle[j])
                    break;
            }
            if(j == len2) return i;
        }
        return -1;
    }
};
```
