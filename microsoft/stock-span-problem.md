# Stock span problem

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/stock-span-problem-1587115621/1#)

The stock span problem is a financial problem where we have a series of n daily price quotes for a stock and we need to calculate the span of stock’s price for all n days. 

The span Si of the stock’s price on a given day i is defined as the maximum number of consecutive days just before the given day, for which the price of the stock on the current day is less than or equal to its price on the given day.

For example, if an array of 7 days prices is given as {100, 80, 60, 70, 60, 75, 85}, then the span values for corresponding 7 days are {1, 1, 1, 2, 1, 4, 6}.

### Sample Input
```
7
100 80 60 70 60 75 85
```

### Sample Output
```
1 1 1 2 1 4 6 
```

### Solution
```cpp
class Solution {
    public:
    vector <int> calculateSpan(int price[], int n)
    {
        stack<int> previous_peak;
        previous_peak.push(0);
        
        vector<int> ans(n);
        ans[0] = 1;

        for(int i = 1; i < n; ++i) {
            while(!previous_peak.empty() && price[previous_peak.top()] <= price[i]) {
                previous_peak.pop();
            }

            ans[i] = i - (previous_peak.empty() ? -1 : previous_peak.top());
            previous_peak.push(i);
        }

        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149402979-a1219d21-6b56-4bb3-b5e4-166dbba28ad7.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=13c879e3f83a1740817b66da69b6e8b6&pid=701342&user=jhasuraj)