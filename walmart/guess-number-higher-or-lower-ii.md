# Guess Number Higher or Lower II

[![Problem Link](../assets/lc.svg)](https://leetcode.com/problems/guess-number-higher-or-lower-ii/)


### Example 1
```
Input: n = 10
Output: 16
```

### Example 2
```
Input: n = 1
Output: 0
```

### Solution
```cpp
class Solution {
public:
    
    int maxAmount(int start, int end, vector<vector<int>> &cache) {
        if(end == start) {
            return 0;
        }
        if(end - start == 1) {
            return min(start, end);
        }
        if(cache[start][end] != -1) return cache[start][end];

        int ans = INT_MAX;
        for(int i = start + 1; i < end; ++i) {
            ans = min(ans, i + max(maxAmount(start, i - 1, cache), maxAmount(i + 1, end, cache)));
        }
        
        cache[start][end] = ans;

        return ans;
    }

    int getMoneyAmount(int n) {
        vector<vector<int>> cache(n + 1, vector<int>(n + 1, -1));
        return maxAmount(1, n, cache);
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151699033-def4ebf7-6ca4-439b-b08e-72f43f59adef.png)](https://leetcode.com/submissions/detail/630897398/)
