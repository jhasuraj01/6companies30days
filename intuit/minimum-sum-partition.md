# Minimum sum partition

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/minimum-sum-partition3317/1/#)

Given an integer array arr of size N, the task is to divide it into two sets S1 and S2 such that the absolute difference between their sums is minimum and find the minimum difference

### DP Table
![image](https://user-images.githubusercontent.com/44930179/148940265-8eb4f3ab-2a6e-413d-94d6-2b5b7e3a83a8.png)

### Sample Input
```
8
5 6 6 5 7 4 7 6
```
### Sample Output
```
0
```

### Solution
```cpp
class Solution {

  public:
	int minDifference(int arr[], int n)  {

	    sort(arr, arr+n);

	    int sum = accumulate(arr, arr + n, 0);
	    
	    int half = sum/2;
	    
	    vector< vector<int> > dp(n + 1, vector<int>(half + 1, 0));
	    
	    for(int i = 0; i < n; ++i) {
	        for(int j = 1; j <= half; ++j) {
	            if(j < arr[i]) {
	                dp[i+1][j] = dp[i][j];
	                continue;
	            }
	            dp[i+1][j] = max({arr[i], dp[i][j - arr[i]] + arr[i], dp[i][j]});
	        }
	    }
	    return sum - dp.back().back()*2;
	}
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148939947-7f0c69cb-e9e0-4318-952d-2e23c48f0100.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=3f5cb6117c6bbc13d452b2aef30dcc85&pid=704140&user=jhasuraj)
