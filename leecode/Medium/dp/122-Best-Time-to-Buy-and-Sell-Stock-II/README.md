## 122	Best Time to Buy and Sell Stock II

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

## Solution

```C++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        /*
        dp[0] = 0
        dp[i] = dp[i-1] + prices[i] - prices[i-1] if prices[i] > prices[i-1]
        dp[i] = dp[i-1] if prices[i] = prices[i-1]
        
        result is prices[n-1]
        */
        int n = prices.size();
        if(n <= 1) return 0;
        vector<int> dp(n, 0);
        dp[0] = 0;
        for(int i=1; i<n; i++){
            if(prices[i] > prices[i-1]) 
                dp[i] = dp[i-1] + prices[i] - prices[i-1];
            else 
                dp[i] = dp[i-1];
        }
        return dp[n-1];
    }
};
```