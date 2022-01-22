# Split Array Largest Sum

[![Problem Link](../assets/lc.svg)](https://leetcode.com/problems/split-array-largest-sum)

Given an array nums which consists of non-negative integers and an integer m, you can split the array into m non-empty continuous subarrays.

Write an algorithm to minimize the largest sum among these m subarrays.

### Example 1
```
Input: nums = [7,2,5,10,8], m = 2
Output: 18
```

### Example 2
```
Input: nums = [1,2,3,4,5], m = 2
Output: 9
```

### Solution
```cpp
class Solution {
public:
    int minLargestSum(vector<int>& nums, int m, int start, int end, vector<int>& presum, vector<vector<int>>& cache) {
        if(m == 1) {
            return presum[end] - presum[start];
        }
        if(cache[start][m] != -1) return cache[start][m];

        int ans = INT_MAX;

        for(int i = start + 1; i <= end - m + 1; ++i) {
            int largest_sum = max(
                presum[i] - presum[start],
                minLargestSum(nums, m - 1, i, end, presum, cache)
            );
            ans = min(ans, largest_sum);
        }

        return cache[start][m] = ans;
    }
    
    int splitArray(vector<int>& nums, int m) {

        vector<int> presum(nums.size() + 1, 0);
        vector<vector<int>> cache(nums.size(), vector<int>(m+1, -1));

        for(int i = 0; i < nums.size(); ++i) {
            presum[i + 1] = presum[i] + nums[i];
        }
        
        return minLargestSum(nums, m, 0, nums.size(), presum, cache);
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/150654222-dcb0b2e5-cd2f-44a2-9015-d8e234b5849e.png)](https://leetcode.com/submissions/detail/625510184/)
