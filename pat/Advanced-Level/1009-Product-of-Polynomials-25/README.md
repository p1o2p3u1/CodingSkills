## 1009. Product of Polynomials (25)
This time, you are supposed to find A*B where A and B are two polynomials.

**Input Specification:**

Each input file contains one test case. Each case occupies 2 lines, and each line contains the information of a polynomial: K N1 aN1 N2 aN2 ... NK aNK, where K is the number of nonzero terms in the polynomial, Ni and aNi (i=1, 2, ..., K) are the exponents and coefficients, respectively. It is given that 1 <= K <= 10, 0 <= NK < ... < N2 < N1 <=1000.

**Output Specification:**

For each test case you should output the product of A and B in one line, with the same format as the input. Notice that there must be NO extra space at the end of each line. Please be accurate up to 1 decimal place.

Sample Input
```
2 1 2.4 0 3.2
2 2 1.5 1 0.5
```
Sample Output
```
3 3 3.6 2 6.0 1 1.6
```

## Solution
有两个坑
1. 指数的取值范围在[0, 1000], 做乘法时指数相加，因此数组应该开到2000
2. 浮点数判断是否不为0还是用`fabs(a) > 1e-6`这种吧
```C++
#include <iostream>
#include <string>
#include <sstream>
#include <map>
#include <cmath>
#include <cstdio>
#include <cstdlib>
using namespace std;
double ans[2001];
int main(){
	fill_n(&ans[0], 2001, 0);
	map<int, double> m1;
	map<int, double> m2;
	int n;
	cin>>n;
	int exp;
	double coef;
	while(n--){
		cin>>exp>>coef;
		m1[exp] = coef;
	}
	cin>>n;
	while(n--){
		cin >> exp >> coef;
		m2[exp] = coef;
	}
	for(auto i = m1.begin(); i != m1.end(); i++){
		for(auto j = m2.begin(); j != m2.end(); j++){
			exp = i -> first + j -> first;
			coef = i -> second * j -> second;
			ans[exp] += coef;
 		}
	}
	int sum = 0;
	for(int i=0; i<2001; i++) if(fabs(ans[i]) > 1e-6) sum++;
	cout<<sum;
	for(int i=2000; i>=0; i--)
		if(fabs(ans[i]) > 1e-6)
			printf(" %d %.1f", i, ans[i]);
	cout<<endl;
	system("pause");
}
```
