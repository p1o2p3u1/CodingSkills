## 121	Best Time to Buy and Sell Stock

Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

## Solution

并不是简单的最大值减去最小值，比如股票一路下跌，最大收益应该是0

sample`[6, 1, 3, 2, 4, 7]`

注意区别II


```C++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        /*
        imin = prices[0];
        dp[0] = 0;
        dp[i] = dp[i-1] + prices[i] - prices[i-1] if prices[i] >= imin
        dp[i] = 0, imin = prices[i] if prices[i] < imin

        result is minimum of dp[]
        */
        if(prices.size() <= 1) return 0;
        vector<int> dp(prices.size(), 0);
        dp[0] = 0;
        int ret = 0;
        int imin = prices[0];
        for(int i=1; i<prices.size(); i++){
            if(prices[i] >= imin){
                dp[i] = dp[i-1] + prices[i] - prices[i-1];
            } else {
                dp[i] = 0;
                imin = prices[i];
            }
            if(dp[i] > ret) ret = dp[i];
        }
        return ret;
    }
};
```