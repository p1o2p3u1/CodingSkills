## 119	Pascal's Triangle II

Given an index k, return the kth row of the Pascal's triangle.

For example, given k = 3,
Return [1,3,3,1].
```
   1
  1 1
 1 2 1
1 3 3 1
```
Note:
Could you optimize your algorithm to use only O(k) extra space?

## Solution

```C++
class Solution {
public:
    vector<int> getRow(int k) {
    	vector<int> ret;
    	if(k < 0) return ret;
    	vector<int> pre;
    	pre.push_back(1);
    	if(k == 0) return pre;
    	for(int i=1; i<=k; i++){
    		ret.push_back(1);
    		for(int j=0; j<i-1; j++){
    			ret.push_back(pre[j] + pre[j+1]);
    		}
    		ret.push_back(1);
    		pre = ret;
    		ret.clear();
    	}
    	return pre;
    }
};
```