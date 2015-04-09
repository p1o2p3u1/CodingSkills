## 46	Permutations
Given a collection of numbers, return all possible permutations.

For example,
```
[1,2,3] 
```
have the following permutations:
```
[1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], and [3,2,1].
```

## Solution
dfs的搜索题
```C++
class Solution {
private:
    void dfs(vector<int> &num, vector<int> &candidate, vector<vector<int> > &ret){
        if(candidate.size() == num.size()){
            ret.push_back(candidate);
            return;
        }
        for(int i=0; i<num.size(); i++){
            auto pos = find(candidate.begin(), candidate.end(), num[i]);
            if(pos == candidate.end()){
                candidate.push_back(num[i]);
                dfs(num, candidate, ret);
                candidate.pop_back();
            }
        }
    }
public:
    vector<vector<int> > permute(vector<int> &num) {
        vector<vector<int> > ret;
        vector<int> candidate;
        dfs(num, candidate, ret);
        return ret;
    }
};
```
