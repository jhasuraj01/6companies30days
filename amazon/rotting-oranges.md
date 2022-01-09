# Rotting Oranges

[![Problem Link](../assets/lc.svg)](https://leetcode.com/problems/rotting-oranges/)

You are given an `m x n` grid where each cell can have one of three values:

- `0` representing an empty cell,
- `1` representing a fresh orange, or
- `2` representing a rotten orange.

Every minute, any fresh orange that is **4-directionally adjacent** to a rotten orange becomes rotten.

Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return `-1`.

 

### Example 1
```
Input: grid = [[2,1,1],[1,1,0],[0,1,1]]
Output: 4
```
### Example 2
```
Input: grid = [[2,1,1],[0,1,1],[1,0,1]]
Output: -1
```

### Solution
```cpp
class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid) {
        
        int M = grid.size();
        int N = grid[0].size();
        
        // store all the fresh mangoes
        vector<pair<int, int>> initially_fresh;

        // store mangoes to be rotten in next sec;
        queue<pair<int, int>> decay_queue;
        
        // queued
        vector<vector<bool>> queued(M, vector<bool>(N, false));
        
        
        for(int i = 0; i < M; ++i) {
            for(int j = 0; j < N; ++j) {
                if(grid[i][j] == 1) {
                    initially_fresh.push_back({i, j});
                }
                else if(grid[i][j] == 2) {
                    decay_queue.push({i, j});
                }
            }
        }
        decay_queue.push({-1, -1});
        
        int sec = -1;

        while(!decay_queue.empty()) {
            pair<int, int> pos = decay_queue.front();
            decay_queue.pop();

            int y = pos.first;
            int x = pos.second;

            if(x == -1 && y == -1) {
                ++sec;
                if(!decay_queue.empty()) {
                    decay_queue.push({-1, -1});
                }
                continue;
            }

            // left
            if(x > 0 && !queued[y][x-1] && grid[y][x-1] == 1) {
                queued[y][x-1] = true;
                decay_queue.push({y, x-1});
            }

            // right
            if(x < N - 1 && !queued[y][x+1] && grid[y][x+1] == 1) {
                queued[y][x+1] = true;
                decay_queue.push({y, x+1});
            }

            // top
            if(y > 0 && !queued[y-1][x] && grid[y-1][x] == 1) {
                queued[y-1][x] = true;
                decay_queue.push({y-1, x});
            }

            // bottom
            if(y < M - 1 && !queued[y+1][x] && grid[y+1][x] == 1) {
                queued[y+1][x] = true;
                decay_queue.push({y+1, x});
            }
        }
        
        for(auto pos: initially_fresh) {
            if(!queued[pos.first][pos.second]) {
                return -1;
            }
        }
        
        return sec;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148677652-1284922d-9e91-4d6f-b2c6-1eb58f525323.png)](https://leetcode.com/submissions/detail/616169791/)
