# Maximum Performance of a Team

[![Problem Link](../assets/lc.svg)](https://leetcode.com/problems/maximum-performance-of-a-team/)

You are given two integers n and k and two integer arrays speed and efficiency both of length n. There are n engineers numbered from 1 to n. speed[i] and efficiency[i] represent the speed and efficiency of the ith engineer respectively.

Choose at most k different engineers out of the n engineers to form a team with the maximum performance.

The performance of a team is the sum of their engineers' speeds multiplied by the minimum efficiency among their engineers.

Return the maximum performance of this team. Since the answer can be a huge number, return it modulo 10<sup>9</sup> + 7.

### Example 1
```
Input: n = 6, speed = [2,10,3,1,5,8], efficiency = [5,4,3,9,7,2], k = 2
Output: 60
```

### Example 2
```
Input: n = 6, speed = [2,10,3,1,5,8], efficiency = [5,4,3,9,7,2], k = 3
Output: 68
```

### Solution
```cpp
class Solution {
public:
    int maxPerformance(int n, vector<int>& speed, vector<int>& efficiency, int k) {
        
        vector<pair<int, int>> eng(n);
        
        long long int MOD = 1e9+7;
        
        for(int i = 0; i < n; ++i) {
            eng[i].first = efficiency[i];
            eng[i].second = speed[i];
        }
        
        sort(eng.rbegin(), eng.rend());
        
        long long int sum = 0;
        long long int ans = INT_MIN;
        
        priority_queue<long long, vector<long long>, greater<long long>> heap;
        
        for(int i = 0; i < k; ++i) {
            heap.push(eng[i].second);
            sum += eng[i].second;
            ans = max(ans, sum*eng[i].first);
        }
        
        for(int i = k; i < n; ++i) {
            heap.push(eng[i].second);
            sum += eng[i].second;
            sum -= heap.top(); heap.pop();
            ans = max(ans, sum*eng[i].first);
        }

        return ans%MOD;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151706026-3e12a8a9-d351-49da-8aa0-8ebea9a9751b.png)](https://leetcode.com/submissions/detail/630982782/)