# Unit Area of largest region of 1's

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/length-of-largest-region-of-1s-1587115620/1/#)

Given a grid of dimension nxm containing 0s and 1s. Find the unit area of the largest region of 1s.

Region of 1's is a group of 1's connected 8-directionally (horizontally, vertically, diagonally).

### Sample Input
```
3 4 
1 1 1 0 
0 0 1 0 
0 0 0 1 
```

### Sample Output
```
5
```

### Solution
```cpp
class Solution {
    public:
    int calc_area(int r, int c, vector<vector<int>>& grid) {

        int R = grid.size() - 1;
        int C = grid[0].size() - 1;

        queue<pair<int, int>> q;
        q.push({r, c});
        grid[r][c] = 0;

        int area = 0;

        while(!q.empty()) {
            ++area;

            pair<int, int> block = q.front();
            r = block.first;
            c = block.second;

            // top
            if(r > 0 && grid[r-1][c] == 1) {
                q.push({r-1, c});
                grid[r-1][c] = 0;
            }

            // right
            if(c < C && grid[r][c+1] == 1) {
                q.push({r, c+1});
                grid[r][c+1] = 0;
            }

            // bottom
            if(r < R && grid[r+1][c] == 1) {
                q.push({r+1, c});
                grid[r+1][c] = 0;
            }

            // left
            if(c > 0 && grid[r][c-1] == 1) {
                q.push({r, c-1});
                grid[r][c-1] = 0;
            }

            // topright
            if(r > 0 && c < C && grid[r-1][c+1] == 1) {
                q.push({r-1, c+1});
                grid[r-1][c+1] = 0;
            }
    
            // bottomright
            if(r < R && c < C && grid[r+1][c+1] == 1) {
                q.push({r+1, c+1});
                grid[r+1][c+1] = 0;
            }

            // bottomleft
            if(r < R && c > 0 && grid[r+1][c-1] == 1) {
                q.push({r+1, c-1});
                grid[r+1][c-1] = 0;
            }

            // topleft
            if(r > 0 && c > 0 && grid[r-1][c-1] == 1) {
                q.push({r-1, c-1});
                grid[r-1][c-1] = 0;
            }

            q.pop();
        }

        return area;
    }

    int findMaxArea(vector<vector<int>>& grid) {
        int max_area = 0;
        queue<int> q;
        
        int n = grid.size();
        int m = grid[0].size();
        
        for(int r = 0; r < n; ++r) {
            for(int c = 0; c < m; ++c) {
                if(grid[r][c]) {
                    max_area = max(max_area, calc_area(r, c, grid));
                }
            }
        }
        
        return max_area;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149300689-c4333ae2-bfc0-42b7-a3bc-72605843b533.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=39b10537fce534f2c18cba0918cff911&pid=701276&user=jhasuraj)
