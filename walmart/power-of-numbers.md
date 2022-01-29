# Power Of Numbers 

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/power-of-numbers-1587115620/1/#)

Given a number and its reverse. Find that number raised to the power of its own reverse.

**Note:** As answers can be very large, print the result modulo 109 + 7.

### Sample Input
```
2
```
### Sample Output
```
4
```

### Solution
```cpp
class Solution {
    public:
    long long MOD = 1e9+7;
    long long power(long long N, long long R)
    {
        N %= MOD;
        long long ans = 1;
        while (R > 0) {
            if (R & 1) {
                ans = (ans * N) % MOD;
            }
            N = (N * N) % MOD;
            R >>= 1;
        }
        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151652677-e4e09f3c-fb47-4964-a2a8-b599625524c0.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=485e8401e3cbaf8158dedc3261e361c8&pid=701195&user=jhasuraj)