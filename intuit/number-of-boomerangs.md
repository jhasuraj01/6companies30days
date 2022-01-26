# Number of Boomerangs

[![Problem Link](../assets/lc.svg)](https://leetcode.com/problems/number-of-boomerangs/)

You are given n points in the plane that are all distinct, where points[i] = [xi, yi]. A boomerang is a tuple of points (i, j, k) such that the distance between i and j equals the distance between i and k (the order of the tuple matters).

Return the number of boomerangs.

### Example 1
```
Input: points = [[0,0],[1,0],[2,0]]
Output: 2
```

### Example 2
```
Input: points = [[1,1],[2,2],[3,3]]
Output: 2
```

### Solution
```cpp
class Solution {
public:
    int squaredDistance(vector<int> &a, vector<int> &b) {
        return (a[0] - b[0])*(a[0] - b[0]) + (a[1] - b[1])*(a[1] - b[1]);
    }

    int numberOfBoomerangs(vector<vector<int>>& points) {
        int len =  points.size();

        vector<unordered_map<int, int>> dist(len);
    
        for(int i = 0; i < len; ++i) {
            for(int j = i + 1; j < len; ++j) {
                int distance = squaredDistance(points[i], points[j]);
                ++dist[i][distance];
                ++dist[j][distance];
            }
        }
        
        int ans = 0;

        for(auto point: dist) {
            for(auto d: point) {
                ans += d.second * (d.second - 1);
            }
        }
        
        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151125945-895a719b-54ce-40fa-b4b8-8782b7e3eb8e.png)](https://leetcode.com/submissions/detail/628125746/)
