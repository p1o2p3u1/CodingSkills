## 38	Count and Say

The count-and-say sequence is the sequence of integers beginning as follows:
`1, 11, 21, 1211, 111221, ...`

`1` is read off as "one 1" or `11`.
`11` is read off as "two 1s" or `21`.
`21` is read off as "one 2, then one 1" or `1211`.
Given an integer n, generate the nth sequence.

Note: The sequence of integers will be represented as a string.

## Solution

nth sequence的下标从1开始。 注意考虑下，当出现类似"eighteen 1s" or `181`的时候，下面的算法就不对了。

```C++
class Solution {
public:
    string countAndSay(int n) {
        if(n == 1) return "1";
        string pre = "1";
        while(n>1){
            string tmp;
            char s[2];
            s[0] = pre[0];
            int sum = 1;
            for(int i=1; i<pre.length(); i++){
                if(pre[i] == s[0]){
                    sum ++;
                }else{
                    tmp += (sum + '0');
                    tmp += s[0];
                    s[0] = pre[i];
                    sum = 1;
                }
            }
            tmp += (sum + '0');
            tmp += s[0];
            pre = tmp;
            n--;
        }
        return pre;
    }
};
```