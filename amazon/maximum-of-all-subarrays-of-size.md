# Maximum of all subarrays of size k

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/maximum-of-all-subarrays-of-size-k3101/1#)

Given an array arr[] of size N and an integer K. Find the maximum for each and every contiguous subarray of size K.

### Sample Input
```
9 3
1 2 3 1 4 5 2 3 6
```
### Sample Output
```
3 3 4 5 5 5 6 
```

### Solution
```cpp
class Solution
{
  public:
    vector <int> max_of_subarrays(int *arr, int n, int k)
    {
        priority_queue<pair<int, int>> MAXQ;

        for(int i = 0; i < k; ++i) {
            MAXQ.push({arr[i], i});
        }
        
        vector<int>ans;
        ans.push_back(MAXQ.top().first);

        for(int i = k; i < n; ++i) {
            MAXQ.push({arr[i], i});
            
            while(!MAXQ.empty() && MAXQ.top().second <= i - k) {
                MAXQ.pop();
            }
            
            ans.push_back(MAXQ.top().first);
        }
        
        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148493994-1f2b8aa2-5acc-4ca1-9048-7e548b101524.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=f51db7b68b8bbbf5f7b26a63716bbc8a&pid=701349&user=jhasuraj)
