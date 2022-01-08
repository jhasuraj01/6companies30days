# Maximum Profit

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/maximum-profit4657/1#)

In the stock market, a person buys a stock and sells it on some future date. Given the stock prices of N days in an array A[ ] and a positive integer K, find out the maximum profit a person can make in at-most K transactions. A transaction is equivalent to (buying + selling) of a stock and new transaction can start only when the previous transaction has been completed.

### DP Table (Hint)
![Hint Table](https://user-images.githubusercontent.com/44930179/148659858-dd45a472-54b3-4561-8bda-b7c35b2df318.png)

### Sample Input
```
2
6
10 22 5 75 65 80
```
### Sample Output
```
87
```

### Solution
```cpp
class Solution {
  public:
    int maxProfit(int K, int N, int A[]) {

        // DP of Transaction Count vs Price
        vector<vector<int>> TP(K+1, vector<int>(N+1, 0));

        for(int t = 1; t <= K; ++t) {
            for(int p = 1; p <= N; ++p) {
                TP[t][p] = TP[t][p - 1];
                for(int i = 0; i < p; ++i) {
                    TP[t][p] = max(TP[t][p], TP[t-1][i] + A[p-1] - A[i]);
                }
            }
        }
        return TP.back().back();
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148659846-1bfc829b-a670-4dcb-bc6c-0b62e57545a5.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=dc89596439fffc05b04dac11f8183b05&pid=704532&user=jhasuraj)
