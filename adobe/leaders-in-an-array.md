# Leaders in an array

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/leaders-in-an-array-1587115620/1/#)

Given an array A of positive integers. Your task is to find the leaders in the array. An element of array is leader if it is greater than or equal to all the elements to its right side. The rightmost element is always a leader. 

### Sample Input
```
6
16 17 4 3 5 2
```
### Sample Output
```
17 5 2
```

### Solution
```cpp
class Solution {
    public:
    vector<int> leaders(int a[], int n){
        vector<int> ans;
        ans.push_back(a[n-1]);

        int max_val = a[n-1];

        for(int i = 1; i < n; ++i){
            if(max_val <= a[n - i - 1]) {
                ans.push_back(a[n - i - 1]);
                max_val = a[n - i - 1];
            }
        }

        reverse(ans.begin(), ans.end());

        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149936214-3a24a285-e15c-4b46-921f-075d501dacef.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=30cfc513c6cf9858e5cc87d1b57fc621&pid=701210&user=jhasuraj)
