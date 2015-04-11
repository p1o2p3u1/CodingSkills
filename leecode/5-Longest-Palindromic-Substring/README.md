## 5	Longest Palindromic Substring
Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.

## Solution
简单解法：以每一个字符为中心向两边扩展，找到最长的回文串
```C++
class Solution {
private:
    string expand(string s, int left, int right){
        if(left <  0 || right >= s.length()) return "";
        while(left >=0 && right < s.length()){
            if(s[left] == s[right]) {
                left --;
                right ++;
            }else break;
        }
        return s.substr(left + 1, right - left - 1);
    }
public:
    string longestPalindrome(string s) {
        string ret,s1;
        for(int i=0; i<s.length(); i++){
            s1 = expand(s, i, i);
			if(s1.length() > ret.length()) ret = s1;
			s1 = expand(s, i, i+1);
			if(s1.length() > ret.length()) ret = s1;
        }
        return ret;
    }
};
```