## 1001. A+B Format (20)
Calculate a + b and output the sum in standard format -- that is, the digits must be separated into groups of three by commas (unless there are less than four digits).

Input

Each input file contains one test case. Each case contains a pair of integers a and b where -1000000 <= a, b <= 1000000. The numbers are separated by a space.

Output

For each test case, you should output the sum of a and b in one line. The sum must be written in the standard format.

Sample Input
```
-1000000 9
```
Sample Output
```
-999,991
```
##Solution

```
#include <string>
#include <iostream>
#include <sstream>
using namespace std;
int main()
{
  int a,b;
  while(cin>>a>>b){
    int sum = a + b;
    stringstream ss;
    ss<<sum;
    string str = ss.str();
    for(int i=str.size()-3; i>0 && str[i-1]!='-'; i-=3)
      str.insert(i,",");
    cout<<str<<endl;
  }
  system("pause");
}
```
