# Partition Equal Subset Sum

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/subset-sum-problem2014/1#)

Given an array arr[] of size N, check if it can be partitioned into two parts such that the sum of elements in both parts is the same.

### Sample Input
```
4
1 5 11 5
```

### Sample Output
```
YES
```

### Solution
```cpp
class Solution {
public:
    int equalPartition(int N, int arr[])
    {
        sort(arr, arr+N);

	    int sum = accumulate(arr, arr + N, 0);

	    if(sum & 1) return 0;

	    int half = sum/2;

	    vector< vector<int> > dp(N + 1, vector<int>(half + 1, 0));

	    for(int i = 0; i < N; ++i) {
	        for(int j = 1; j <= half; ++j) {
	            if(j < arr[i]) {
	                dp[i+1][j] = dp[i][j];
	                continue;
	            }
	            dp[i+1][j] = max({arr[i], dp[i][j - arr[i]] + arr[i], dp[i][j]});
	        }
	    }

        return half == dp.back().back();
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149914751-fb72b8ce-401c-488a-af1b-437f7814b353.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=79146ffebcac12b5415bb299da721cbf&pid=704573&user=jhasuraj)
