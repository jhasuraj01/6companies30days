# Minimum Size Subarray Sum

[![Problem Link](https://img.shields.io/badge/-LeetCode-FFA116?style=for-the-badge&logo=LeetCode&logoColor=black)](https://leetcode.com/problems/minimum-size-subarray-sum)

Given an array of positive integers nums and a positive integer target, return the minimal length of a contiguous subarray [numsl, numsl+1, ..., numsr-1, numsr] of which the sum is greater than or equal to target. If there is no such subarray, return 0 instead.

### Example 1
```
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
```

### Example 2
```
Input: target = 4, nums = [1,4,4]
Output: 1
```

### Solution
```cpp
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        long long sum = 0;
        int left = 0, right = 0;
        int min_size = INT_MAX;
        
        for(int n: nums) {
            
            sum += n;

            while (sum >= target) {
                min_size = min(min_size, right - left + 1);
                sum -= nums[left++];
            }

            ++right;
        }

        return min_size == INT_MAX ? 0 : min_size;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/147901132-fe09ff41-da3a-4dd7-bc9b-7217b200a877.png)](https://leetcode.com/submissions/detail/611916014/)
