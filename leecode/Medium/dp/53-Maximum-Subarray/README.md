## 53	Maximum Subarray
Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array [−2,1,−3,4,−1,2,1,−5,4],
the contiguous subarray [4,−1,2,1] has the largest sum = 6.

## Solution

```C++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        /*
        dp[0] = nums[0];
        dp[i] = max(dp[i-1] + nums[i], nums[i]);
        
        return max of dp[]
        */
        if(nums.size() == 0) return 0;
        vector<int> dp(nums.size(), 0);
        dp[0] = nums[0];
        int ret = dp[0];
        for(int i=1; i<nums.size(); i++){
            dp[i] = max(dp[i-1] + nums[i], nums[i]);
            ret = max(ret, dp[i]);
        }
        return ret;
    }
};
```
