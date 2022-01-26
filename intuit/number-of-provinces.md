# Number of Provinces

[![Problem Link](../assets/lc.svg)](https://leetcode.com/problems/number-of-provinces/)

There are n cities. Some of them are connected, while some are not. If city a is connected directly with city b, and city b is connected directly with city c, then city a is connected indirectly with city c.

A province is a group of directly or indirectly connected cities and no other cities outside of the group.

You are given an n x n matrix isConnected where isConnected[i][j] = 1 if the ith city and the jth city are directly connected, and isConnected[i][j] = 0 otherwise.

Return the total number of provinces.

### Example 1
```
Input: isConnected = [[1,1,0],[1,1,0],[0,0,1]]
Output: 2
```

### Example 2
```
Input: isConnected = [[1,0,0],[0,1,0],[0,0,1]]
Output: 3
```

### Solution
```cpp
class Solution {
public:
    int findCircleNum(vector<vector<int>>& isConnected) {
        int N = isConnected.size();

        vector<bool> visited(N, false);

        queue<int> line;

        int province = 0;

        for(int r = 0; r < N; ++r) {
            if(visited[r]) continue;

            line.push(r);
            visited[r] = true;
            
            while(!line.empty()) {
                int current = line.front(); line.pop();
                for(int c = 0; c < N; ++c) {
                    if(isConnected[c][current] && !visited[c]) {
                        line.push(c);
                        visited[c] = true;
                    }
                }
            }

            ++province;
        }
        
        return province;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151139117-099ddfe9-124c-4ab8-9aeb-7ca40906eefe.png)](https://leetcode.com/submissions/detail/628166090/)
