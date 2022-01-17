# Subarray with given sum

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/subarray-with-given-sum-1587115621/1#)

Given an unsorted array A of size N that contains only non-negative integers, find a continuous sub-array which adds to a given number S.

### Sample Input
```
5 12
1 2 3 7 5
```
### Sample Output
```
2 4
```

### Solution
```cpp
class Solution {
    public:
    vector<int> subarraySum(int arr[], int n, long long s) {

        int left = 0, right = 0;
        long long sum = (long long) arr[0];
        int changed = true;

        while(changed) {
            changed = false;
            while(left < n && sum > s) {
                sum -= (long long) arr[left];
                ++left;
                changed = true;
            }
            while(right < n - 1 && sum < s) {
                ++right;
                sum += (long long) arr[right];
                changed = true;
            }
            if(sum == s) {
                break;
            }
        }

        if(sum == s) {
            vector<int> ans(2, 0);
            ans[0] = left + 1;
            ans[1] = right + 1;
            return ans;
        }
        else {
            vector<int> ans(1, -1);
            return ans;
        }
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149839962-278fc9a3-59f6-4508-b27e-86ec5b7c9130.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=3778e89d9233ab281349b66e10679d68&pid=701236&user=jhasuraj)
