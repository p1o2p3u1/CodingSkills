## 118	Pascal's Triangle

Given numRows, generate the first numRows of Pascal's triangle.

For example, given numRows = 5,
Return
```
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

## Solution
```C++
class Solution {
public:
    vector<vector<int> > generate(int numRows) {
    	vector<vector<int> > ret;
    	if(numRows<=0) return ret;
    	ret.push_back({1});
    	for(int i=2; i<=numRows; i++){
    		vector<int> tmp;
    		tmp.push_back(1);
    		for(int j=0; j<i-2; j++)
    			tmp.push_back(ret[i-2][j] + ret[i-2][j+1]);
    		tmp.push_back(1);
    		ret.push_back(tmp);
    	}
    	return ret;
    }
};
```