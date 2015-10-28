# 	204	Count Primes
Count the number of prime numbers less than a non-negative number, n

# Solution
筛法选素数，线性查找肯定会超时
```C++
class Solution {
private:
	bool isPrime(int n){
		int d = (int) sqrt(n);
		for(int i=2; i<=d; i++)
			if(n % d == 0)
				return false;
		return true;
	}
public:
    int countPrimes(int n) {
        bool *marked = new bool[n];
        fill_n(marked, n, false);
        int ret = 0;
        for(int i=2; i<n; i++){
            if(!marked[i]){
                if(isPrime(i)){
                    ret += 1;
                    for(int j=1; j * i <= n; j++)
                        marked[j*i] = true;
                }
            }
        }
        return ret;
    }
};
```