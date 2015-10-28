## 168	Excel Sheet Column Title

Given a positive integer, return its corresponding column title as appear in an Excel sheet.

For example:
```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
```

## Solution
字符串插入可以`s.insert(s.begin(), 'c');`，或者`s = 'c'+s;`

```C++
class Solution {
public:
    string convertToTitle(int n) {
        string ret;
        while(n){
            char c;
            if(n % 26 == 0){
                c = 'Z';
                n = n / 26 - 1;
            }else{
                c = n % 26 -1 + 'A';
                n = n / 26;
            }
            ret.insert(ret.begin(), c);
        }
        return ret;
    }
};
```