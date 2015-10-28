# 	205	Isomorphic Strings

Given two strings s and t, determine if they are isomorphic.

Two strings are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

For example,
Given "egg", "add", return true.

Given "foo", "bar", return false.

Given "paper", "title", return true.

Note:
You may assume both s and t have the same length.

# Solution
将字符串映射到一个新字符串，比较新字符串。比如
egg -> 011 add -> 011 true
foo -> 011 bar -> 012 false
paper -> 01023 title -> 01023 true
```C++
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        if(s.length() != t.length()) return false;
        unordered_map<char, int> m_s;
        unordered_map<char, int> m_t;
        string s1, s2; int i=1, j=1;
        for(int k=0; k<s.length(); k++){
            if(m_s.find(s[k]) == m_s.end())
                m_s[s[k]] = i++;
            s1 += m_s[s[k]];
            
            if(m_t.find(t[k]) == m_t.end()){
                m_t[t[k]] = j++;
            }
            s2 += m_t[t[k]];
        }
        return s1 == s2;
    }
};
```