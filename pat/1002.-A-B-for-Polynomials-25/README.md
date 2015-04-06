## 1002. A+B for Polynomials (25)
This time, you are supposed to find A+B where A and B are two polynomials.

Input

Each input file contains one test case. Each case occupies 2 lines, and each line contains the information of a polynomial: K N1 aN1 N2 aN2 ... NK aNK, where K is the number of nonzero terms in the polynomial, Ni and aNi (i=1, 2, ..., K) are the exponents and coefficients, respectively. It is given that 1 <= K <= 10，0 <= NK < ... < N2 < N1 <=1000.

Output

For each test case you should output the sum of A and B in one line, with the same format as the input. Notice that there must be NO extra space at the end of each line. Please be accurate to 1 decimal place.

Sample Input
```
2 1 2.4 0 3.2
2 2 1.5 1 0.5
```
Sample Output
```
3 2 1.5 1 2.9 0 3.2
```

## Solution
有几个坑：

1. 输入的次数项可能有重复，比如 `2 1 1.1 1 1.2`

2. 系数项会有负数，浮点数的比较不要用等号
```C++
#include<cstdio>
#include<cmath>
#include<cstdlib>
using namespace std;
float f[1001];
int main()
{
  fill_n(&f[0], 1001, 0);
  int n;
  scanf("%d", &n);
  int exp;
  float coef;
  while(n--){
    scanf("%d %f", &exp, &coef);
    f[exp] = coef;
  }
  scanf("%d", &n);
  while(n--){
    scanf("%d %f", &exp, &coef);
    f[exp] += coef;  
  }
  int sum = 0;
  for(int i=0; i<1001; i++)
    if(fabs(f[i]) > 1e-6) sum ++;
  printf("%d", sum);
  for(int i=1000; i>=0; i--)
    if(fabs(f[i]) > 1e-6)
      printf(" %d %.1f", i, f[i]);
  printf("\n");
  system("pause");
}
```
