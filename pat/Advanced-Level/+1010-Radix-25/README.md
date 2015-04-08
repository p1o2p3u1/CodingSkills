## 1010. Radix (25)
Given a pair of positive integers, for example, 6 and 110, can this equation 6 = 110 be true? The answer is "yes", if 6 is a decimal number and 110 is a binary number.

Now for any pair of positive integers N1 and N2, your task is to find the radix of one number while that of the other is given.

**Input Specification:**

Each input file contains one test case. Each case occupies a line which contains 4 positive integers:
N1 N2 tag radix
Here N1 and N2 each has no more than 10 digits. A digit is less than its radix and is chosen from the set {0-9, a-z} where 0-9 represent the decimal numbers 0-9, and a-z represent the decimal numbers 10-35. The last number "radix" is the radix of N1 if "tag" is 1, or of N2 if "tag" is 2.

**Output Specification:**

For each test case, print in one line the radix of the other number so that the equation N1 = N2 is true. If the equation is impossible, print "Impossible". If the solution is not unique, output the smallest possible radix.

Sample Input 1:
```
6 110 1 10
```
Sample Output 1:
```
2
```
Sample Input 2:
```
1 ab 1 2
```
Sample Output 2:
```
Impossible
```

## Solution
有很多坑，只能得19分
```C++
#include <iostream>
#include <string>
#include <sstream>
#include <map>
#include<cmath>
#include<cstdio>
#include<cstdlib>
using namespace std;
int R[256];

void init(){
	fill_n(&R[0], 256, 0);
	for(int i='0', j=0; i<='9'; i++,j++) R[i] = j;
	for(int i = 'a', j=10; i<='z'; i++, j++) R[i] = j;
}

long long foo(string str, int radix){
	long long ret = 0;
	int n = str.length()-1;
	for(int i=0; i<str.length(); i++)
		ret += R[str[i]] * pow(radix, n--);
	return ret;
}

int check(long long d, string str){
	for(int i=2; i<=36; i++){
		long long tmp = d;
		int n = str.length() - 1;
		while(tmp){
			if(n >= 0 && tmp % i == R[str[n--]])
				tmp /= i;
			else
				break;
		}
		if(n == -1 && tmp == 0) return i;
	}
	return -1;
}

int main(){
	
	init();
	int flag, radix;
	string n1, n2;
	cin >> n1 >> n2 >> flag >> radix;
	long long d;
	int ret;
	if(flag == 1){
		d = foo(n1, radix);
		ret = check(d, n2);
	}else{
		d = foo(n2, radix);
		ret = check(d, n1);
	}
	if(ret == -1) cout<<"Impossible"<<endl;
	else cout<<ret<<endl;
	system("pause");
}
```
