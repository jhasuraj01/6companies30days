# Number of distict Words with k maximum contiguous vowels

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/7b9d245852bd8caf8a27d6d3961429f0a2b245f1/1/#)

Find the number of unique words consisting of lowercase alphabets only of length N that can be formed with at-most K contiguous vowels. 

### Hint
![image](https://user-images.githubusercontent.com/44930179/150683170-7a2c810c-8971-4f6f-b595-0b63763364f5.png)


### Sample Input
```
384 71
```
### Sample Output
```
233867288
```

### Solution
```cpp
class Solution {
  public:
    int kvowelwords(int N, int K) {
        
        long long int mod = 1000000007;

        vector<vector<int>> dp(N, vector<int>(K + 1, 0));
        dp[0][0] = 21;
        long long int sum = 21;

        if(K > 0) {
            dp[0][1] = 5;
            sum += 5;
        };

        for(int n = 1; n < N; ++n) {
            sum = dp[n][0] = (sum * 21ll) % mod;
            for(int k = 1; k <= K; ++k) {
                sum += dp[n][k] = (dp[n - 1][k - 1]*5ll) % mod;
                sum %= mod;
            }
        }

        return sum;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/150682997-4ab3d559-ff4a-4bf3-bb9f-0a840a4eb243.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=622a9ee7a7bafca6b842bae328ed29d9&pid=706392&user=jhasuraj)
