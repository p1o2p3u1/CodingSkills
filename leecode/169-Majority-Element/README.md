## 169	Majority Element

Given an array of size n, find the majority element. The majority element is the element that appears more than n/2 times.

You may assume that the array is non-empty and the majority element always exist in the array.

## Solution
```C++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        unordered_map<int, int> m;
        const int d = nums.size() / 2;
        for(int i=0; i<nums.size(); i++){
            if(m.find(nums[i]) == m.end())
                m[nums[i]] = 1;
            else
                m[nums[i]] += 1;
            if(m[nums[i]] > d) return nums[i];
        }
    }
};
```
