## 9	Palindrome Number	

Determine whether an integer is a palindrome. Do this without extra space.

## Solution

逆转整数然后与原来的数做比较
```C++
class Solution {
public:
    bool isPalindrome(int x) {
        if(x < 0) return false;
        int d = x;
        int sum = 0;
        while(d){
        	sum = sum * 10 + d % 10;
        	d = d / 10;
    	}
        return x == sum;
    }
};
```

逆转一半的整数，然后与前一半做比较
```
class Solution{
public:
	bool isPalindrome(int x){
		if(x < 0 || x % 10 == 0) return false; // 最后一位必须是非0，0除外。
		int sum = 0;
		while(x > sum){
			sum = sum * 10 + x % 10;
			x /= 10;
		}
		return x == sum || x/10 == sum;
	}
};
```