## 125	Valid Palindrome

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

For example,
"A man, a plan, a canal: Panama" is a palindrome.
"race a car" is not a palindrome.

Note:
Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.

## Solution
迭代版本
```C++
class Solution {
private:
    bool isAlpha(char c){
        if(c >='a' && c<='z') return true;
        else if(c >='A' && c <='Z') return true;
        else if(c >='0' && c <='9') return true;
        else return false;
    }
    char lower(char c){
        if(c>='A' && c <= 'Z') return c - 'A' + 'a';
        else return c;
    }
public:
    bool isPalindrome(string s) {
        int i=0, j=s.length() - 1;
        while(i <= j){
            while(i<=j && !isAlpha(s[i])) i++;
            while(i <= j && !isAlpha(s[j])) j--;
            if(i > j) return true;
            if(lower(s[i]) != lower(s[j])) return false;
            i++;
            j--;
        }
        return true;
    }
    
};
```
递归版本会导致MLE。。
```C++
class Solution {
private:
    bool isAlpha(char c){
        if(c >='a' && c<='z') return true;
        else if(c >='A' && c <='Z') return true;
        else if(c >='0' && c <='9') return true;
        else return false;
    }
    char lower(char c){
        if(c>='A' && c <= 'Z') return c - 'A' + 'a';
        else return c;
    }
    bool isPalindrome(string str, int s, int e){
        if(s >= e) return true;
        while(s <= e && !isAlpha(str[s])) s++;
        while(s <= e && !isAlpha(str[e])) e--;
        if(s > e) return true;
        if(lower(str[s]) != lower(str[e])) return false;
        return isPalindrome(str, s+1, e-1);
    }
public:
    bool isPalindrome(string s) {
        return isPalindrome(s, 0, s.length() - 1);
    }
    
};
```