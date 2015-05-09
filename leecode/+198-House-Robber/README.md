## 198	House Robber

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

## Solution

简单的贪心问题。
1. 当n==1的时候，只需要抢f[1] = s[0]
2. 当n==2的时候，需要抢f[2] = max(s[0], s[1]);
3. 当n==3的时候，需要抢f[3] = max(s[0] + s[2], s[1]);
4. 当n==4的时候，需要抢f[4] = max(f[2] + s[3], f[3]);
5. 当n==k的时候，需要抢f[k] = max(f[k-2] + s[k-1], f[k-1]);

```C
int max(int a, int b){
    return a>b? a:b;
}
int rob(int* s, int numsSize) {
    if(numsSize == 0) return 0;
    if(numsSize == 1) return s[0];
    if(numsSize == 2) return max(s[0], s[1]);
    if(numsSize == 3) return max(s[0] + s[2], s[1]);
    int *f = (int*)malloc(sizeof(int) * (numsSize + 1));
    f[1] = s[0]; f[2] = max(s[0], s[1]); f[3] = max(s[0] + s[2], s[1]);
    for(int k=4; k<=numsSize; k++){
        f[k] = max(f[k-2] + s[k-1], f[k-1]);
    }
    return f[numsSize];
}
```
上面的算法空间复杂度为O(n),实际上可以在O(1)的空间复杂度内解决这个问题，因为每次比较的时候，都只需要比较`max(f[k-2] + s[k-1], f[k-1])`，而再往前的都用不上了。
