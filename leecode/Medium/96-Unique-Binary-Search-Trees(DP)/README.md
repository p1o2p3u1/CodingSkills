## 96	Unique Binary Search Trees

Given n, how many structurally unique BST's (binary search trees) that store values 1...n?

For example,
Given n = 3, there are a total of 5 unique BST's.

```
   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```


## Solution

当n==0时，空树只有一个
当n==1时，根节点只有一个
当n==2时，dp[2] = dp[0] * dp[1] + dp[1] * dp[0]
当n==3时，dp[3] = dp[0] * dp[2] + dp[1] * dp[1] + dp[2] * dp[0]

```C++
int uniqueBST(int n){
	if(n <= 0) return 1;
	vector<int> dp(n+1, 0);
	dp[0] = 1;
	dp[1] = 1;
	for(int i=2; i<=n; i++){
		dp[i] = 0;
		for(int k=0; k<i; k++){
			dp[i] += (dp[k] * dp[i-k-1]);
		}
	}
	return dp[n];
}
```