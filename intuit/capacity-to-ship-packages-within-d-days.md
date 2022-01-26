# Capacity To Ship Packages Within D Days

[![Problem Link](../assets/lc.svg)](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/)

A conveyor belt has packages that must be shipped from one port to another within days days.

The ith package on the conveyor belt has a weight of weights[i]. Each day, we load the ship with packages on the conveyor belt (in the order given by weights). We may not load more weight than the maximum weight capacity of the ship.

Return the least weight capacity of the ship that will result in all the packages on the conveyor belt being shipped within days days.

### Example 1
```
Input: weights = [1,2,3,4,5,6,7,8,9,10], days = 5
Output: 15
```

### Example 2
```
Input: weights = [3,2,2,4,1,4], days = 3
Output: 6
```

### Solution
```cpp
class Solution {
public:
    int minLargestSum(vector<int>& array, int m, int start, int end, vector<int>& presum, vector<vector<int>>& cache) {
        if(m == 1) {
            return presum[end] - presum[start];
        }
        if(cache[start][m] != -1) return cache[start][m];

        int ans = INT_MAX;

        for(int i = start + 1; i <= end - m + 1; ++i) {
            int largest_sum = max(
                presum[i] - presum[start],
                minLargestSum(array, m - 1, i, end, presum, cache)
            );
            ans = min(ans, largest_sum);
        }

        return cache[start][m] = ans;
    }

    int shipWithinDays(vector<int>& weights, int days) {
        vector<int> presum(weights.size() + 1, 0);
        vector<vector<int>> cache(weights.size(), vector<int>(days+1, -1));

        for(int i = 0; i < weights.size(); ++i) {
            presum[i + 1] = presum[i] + weights[i];
        }
        
        return minLargestSum(weights, days, 0, weights.size(), presum, cache);
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151111943-015d5eea-9ba3-4d9c-8af3-2736eee9110b.png)](https://leetcode.com/submissions/detail/627778447/)