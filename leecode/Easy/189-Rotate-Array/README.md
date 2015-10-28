## 189	Rotate Array

Rotate an array of n elements to the right by k steps.

For example, with `n = 7` and `k = 3`, the array `[1,2,3,4,5,6,7]` is rotated to `[5,6,7,1,2,3,4]`.

Note:
Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.

## Solution
时间复杂度O(n), 空间复杂度O(1)
```C++
class Solution {
public:
    void rotate(int nums[], int n, int k) {
        k = k % n;
    	if(n == 0 || k <= 0) return;
    	reverse(nums, 0, n-k);
		reverse(nums, n-k+1, n-1);
		reverse(nums, 0, n-1);
    }
};
```

时间复杂度O(n)，空间复杂度O(n)
```C++
class Solution {
public:
    void rotate(int nums[], int n, int k) {
        k = k % n;
    	if(n == 0 || k <= 0) return;
    	vector<int> tmp;
    	for(int i=0; i<n; i++) 
    		tmp.push_back(nums[i]);
    	for(int i=n-k-1; i>=0; i--) 
    		nums[i+k] = nums[i];
    	for(int i=0; i<k; i++) 
    		nums[i] = tmp[n-k+i];
    }
};
```