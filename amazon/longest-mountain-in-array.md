# Longest Mountain in Array

[![Problem Link](../assets/lc.svg)](https://leetcode.com/problems/longest-mountain-in-array/)

You may recall that an array arr is a mountain array if and only if:

- arr.length >= 3
- There exists some index i (0-indexed) with 0 < i < arr.length - 1 such that:
  - arr[0] < arr[1] < ... < arr[i - 1] < arr[i]
  - arr[i] > arr[i + 1] > ... > arr[arr.length - 1]

Given an integer array arr, return the length of the longest subarray, which is a mountain. Return 0 if there is no mountain subarray.

### Example 1
```
Input: arr = [2,1,4,7,3,2,5]
Output: 5
```
### Example 2
```
Input: arr = [2,2,2]
Output: 0
```

### Solution
```cpp
class Solution {
public:
    bool isLocalMin(vector<int>& arr, int index) {
        int lastIndex = arr.size() - 1;

        if(index == 0) {
            return arr[0] < arr[1];
        }
        else if(index == lastIndex) {
            return arr[lastIndex - 1] > arr[lastIndex];
        }
        else {
            return arr[index - 1] >= arr[index] && arr[index] <= arr[index + 1];
        }
    }
    bool isLocalMax(vector<int>& arr, int index) {
        int lastIndex = arr.size() - 1;

        if(index == 0) {
            return arr[0] > arr[1];
        }
        else if(index == lastIndex) {
            return arr[lastIndex - 1] < arr[lastIndex];
        }
        else {
            return arr[index - 1] < arr[index] && arr[index] > arr[index + 1];
        }
    }
    int longestMountain(vector<int>& arr) {
        
        if(arr.size() < 3) return 0;
        
        int ans = 0;
        int lastLocalMin = -1;
        int lastLocalMax = -1;
        
        for(int i = 0; i < arr.size(); ++i) {
            if(isLocalMin(arr, i)) {
                if(lastLocalMin >= 0 && lastLocalMin < lastLocalMax && lastLocalMax < i) {
                    ans = max(ans, i - lastLocalMin + 1);
                }
                lastLocalMin = i;
            }
            else if(isLocalMax(arr, i)) {
                lastLocalMax = i;
            }
        }

        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148407620-d7fffa63-1177-4a3e-b51d-f9f98b27fb97.png)](https://leetcode.com/submissions/detail/614306576/)
