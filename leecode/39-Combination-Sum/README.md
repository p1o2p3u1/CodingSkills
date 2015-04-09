## 39	Combination Sum

Given a set of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

The same repeated number may be chosen from C unlimited number of times.

Note:
All numbers (including target) will be positive integers.
Elements in a combination `(a1, a2, … , ak)` must be in non-descending order. `(ie, a1 ≤ a2 ≤ … ≤ ak)`.
The solution set must not contain duplicate combinations.
For example, given candidate set `2,3,6,7` and target `7`, 
A solution set is: 
```
[7] 
[2, 2, 3] 
```

## Solution
搜索类的题，不要用模拟
```C++
class Solution {
private:
    void dfs(vector<int> &nums, int target, int start, vector<int> &candidate, vector<vector<int> > &ret){
        if(target == 0 && candidate.size() > 0){
            ret.push_back(candidate);
            return;
        }
        for(int i=start; i<nums.size(); i++){
            if(target < nums[i]) return;
            candidate.push_back(nums[i]);
            dfs(nums, target - nums[i], i, candidate, ret);
            candidate.pop_back();
        }
    }
public:
    vector<vector<int> > combinationSum(vector<int> &nums, int target) {
        sort(nums.begin(), nums.end());
        vector<vector<int> > ret;
        vector<int> candidate;
        dfs(nums, target, 0, candidate, ret);
        return ret;
    }
};
```
