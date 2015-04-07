## 1005. Spell It Right (20)
Given a non-negative integer N, your task is to compute the sum of all the digits of N, and output every digit of the sum in English.

Input Specification:

Each input file contains one test case. Each case occupies one line which contains an N (<= 10100).

Output Specification:

For each test case, output in one line the digits of the sum in English words. There must be one space between two consecutive words, but no extra space at the end of a line.

Sample Input:
```
12345
```
Sample Output:
```
one five
```

## Solution
```C++
#include<iostream>
#include<string>
#include<sstream>
using namespace std;

int main(){
  string map[] = {"zero", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine"};
  string str;
  cin>>str;
  int sum = 0;
  for(int i=0; i<str.length(); i++) sum += str[i] - '0';
  stringstream ss;
  ss << sum;
  string result = ss.str();
  cout<<map[result[0] - '0'];
  for(int i=1; i<result.length(); i++){
    cout<<" "<<map[result[i] - '0'];
  }
  cout<<endl;
  return 0;
}
```
