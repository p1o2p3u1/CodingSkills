## 40	Combination Sum II

Given a collection of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

Each number in C may only be used once in the combination.

Note:
All numbers (including target) will be positive integers.
Elements in a combination `(a1, a2, … , ak)` must be in non-descending order. `(ie, a1 ≤ a2 ≤ … ≤ ak)`.
The solution set must not contain duplicate combinations.
For example, given candidate set `10,1,2,7,6,1,5` and target `8`, 
A solution set is: 
```
[1, 7] 
[1, 2, 5] 
[2, 6] 
[1, 1, 6]
```

## Solution
与Combination Sum类似，只不过一个元素不能取任意次了。
```C++
class Solution {
private:
    void dfs(vector<int> &num, int target, int start, vector<int> &candidate, vector<vector<int> > &ret){
        if(target == 0 && candidate.size() > 0){
            ret.push_back(candidate);
            return;
        }
        for(int i=start; i<num.size(); i++){
            if(target < num[i]) return;
            // 注意 [1,1], 1 这种情况，候选candidate只能出现一次
            if(i && num[i] == num[i-1] && i > start) continue;
            candidate.push_back(num[i]);
            dfs(num, target - num[i], i+1, candidate, ret);
            candidate.pop_back();
        }
    }
public:
    vector<vector<int> > combinationSum2(vector<int> &num, int target) {
        sort(num.begin(), num.end());
        vector<vector<int> > ret;
        vector<int> candidate;
        dfs(num, target, 0, candidate, ret);
        return ret;
    }
};
```
