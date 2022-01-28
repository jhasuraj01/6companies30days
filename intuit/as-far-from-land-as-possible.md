# As Far from Land as Possible

[![Problem Link](../assets/lc.svg)](https://leetcode.com/problems/as-far-from-land-as-possible/)

Given an n x n grid containing only values 0 and 1, where 0 represents water and 1 represents land, find a water cell such that its distance to the nearest land cell is maximized, and return the distance. If no land or water exists in the grid, return -1.

The distance used in this problem is the Manhattan distance: the distance between two cells (x0, y0) and (x1, y1) is |x0 - x1| + |y0 - y1|.

### Example 1
```
Input: grid = [[1,0,1],[0,0,0],[1,0,1]]
Output: 2
```

### Example 2
```
Input: grid = [[1,0,0],[0,0,0],[0,0,0]]
Output: 4
```

### Solution
```cpp
class Solution {
public:
    void bfs(int ROW, int COL, queue<vector<int>> &line, vector<vector<int>>& distance) {
        while(!line.empty()) {
            vector<int> current_cell = line.front(); line.pop();
            int row = current_cell[0];
            int col = current_cell[1];
            int dis = current_cell[2];

            dis = distance[row][col] = min(dis, distance[row][col]);

            //top
            if(row > 0 && (dis + 1) < distance[row - 1][ col]) {
                line.push({row - 1, col, dis + 1});
            }

            //right
            if(col < (COL - 1 )&& (dis + 1) < distance[row][col + 1]) {
                line.push({row, col + 1, dis + 1});
            }

            //bottom
            if(row < (ROW - 1) && (dis + 1) < distance[row + 1][col]) {
                line.push({row + 1, col, dis + 1});
            }

            //left
            if(col > 0 && (dis + 1) < distance[row][col - 1]) {
                line.push({row, col - 1, dis + 1});
            }
        }
    }

    int maxDistance(vector<vector<int>>& grid) {
        int ROW = grid.size();
        int COL = grid[0].size();

        vector<vector<int>> distance(ROW, vector<int>(COL, INT_MAX));
        queue<vector<int>> line;

        int ans = 0;
        for(int i = 0; i < ROW; ++i) {
            for(int j = 0; j < COL; ++j) {
                if(grid[i][j]) {
                    line.push({i, j, 0});
                };
            }
        }

        bfs(ROW, COL, line, distance);

        for(int i = 0; i < ROW; ++i) {
            for(int j = 0; j < COL; ++j) {
                ans = max(ans, distance[i][j]);
            }
        }

        return (ans == 0 || ans == INT_MAX ? -1 : ans);
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151479642-71c1f7c9-aae9-475e-9a42-10bb91f7e8d9.png)](https://leetcode.com/submissions/detail/629321714/)
