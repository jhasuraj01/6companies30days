# Express as sum of power of natural numbers

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/express-as-sum-of-power-of-natural-numbers5647/1#)

Given two numbers n and x, find out the total number of ways n can be expressed as sum of xth power of unique natural numbers.As total number of ways can be very large ,so return the number of ways modulo 10<sup>9</sup> + 7.

### Sample Input
```
1
10 2
```

### Sample Output
```
1
```

### Solution
```cpp
class Solution {
    public:
    long long int mod = 1e9+7;
    long long int dp[1001][1002];
    long long int count(int n, int x, int k)
    {
        if(n == 0) return 1;
        if(n < 0) return 0;
        if(k > n) return 0;

        if(dp[n][k] != -1) return dp[n][k];

        long long int ans = count(n - pow(k, x), x, k + 1) + count(n, x, k + 1);

        dp[n][k] = ans %= mod;

        return ans;
    }

    int numOfWays(int n, int x)
    {
        memset(dp, -1, sizeof(dp));
        return count(n, x, 1);
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/150784263-a4e315f8-f471-486c-bbab-9048566e7d78.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=10d297f717e185552ea45f41da740c21&pid=705641&user=jhasuraj)