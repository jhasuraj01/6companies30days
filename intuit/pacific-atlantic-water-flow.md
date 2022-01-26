# Pacific Atlantic Water Flow

[![Problem Link](../assets/lc.svg)](https://leetcode.com/problems/pacific-atlantic-water-flow/)

There is an m x n rectangular island that borders both the Pacific Ocean and Atlantic Ocean. The Pacific Ocean touches the island's left and top edges, and the Atlantic Ocean touches the island's right and bottom edges.

The island is partitioned into a grid of square cells. You are given an m x n integer matrix heights where heights[r][c] represents the height above sea level of the cell at coordinate (r, c).

The island receives a lot of rain, and the rain water can flow to neighboring cells directly north, south, east, and west if the neighboring cell's height is less than or equal to the current cell's height. Water can flow from any cell adjacent to an ocean into the ocean.

Return a 2D list of grid coordinates result where result[i] = [ri, ci] denotes that rain water can flow from cell (ri, ci) to both the Pacific and Atlantic oceans.

### Example 1
```
Input: heights = [[1,2,2,3,5],[3,2,3,4,4],[2,4,5,3,1],[6,7,1,4,5],[5,1,1,2,4]]
Output: [[0,4],[1,3],[1,4],[2,2],[3,0],[3,1],[4,0]]
```

### Example 2
```
Input: heights = [[2,1],[1,2]]
Output: [[0,0],[0,1],[1,0],[1,1]]
```

### Solution
```cpp
class Solution {
public:
    
    void pacificBFS(int row, int col, vector<vector<int>>& heights, vector<vector<int>>& visited) {
        
        int m = heights.size();
        int n = heights[0].size();

        if(visited[row][col] == 1) {
            return;
        }

        queue<pair<int, int>> pq;

        pq.push({row, col});
        visited[row][col] = 1;

        while(!pq.empty()) {

            pair current = pq.front(); pq.pop();

            int row = current.first;
            int col = current.second;
            int height = heights[row][col];

            // top
            if(row > 0 && visited[row - 1][col] != 1 && heights[row - 1][col] >= height) {
                pq.push({row - 1, col});
                visited[row - 1][col] = 1;
            }

            // left
            if(col > 0 && visited[row][col - 1] != 1 && heights[row][col - 1] >= height) {
                pq.push({row, col - 1});
                visited[row][col - 1] = 1;
            }

            // right
            if(col < n - 1 && visited[row][col + 1] != 1 && heights[row][col + 1] >= height) {
                pq.push({row, col + 1});
                visited[row][col + 1] = 1;
            }

            // bottom
            if(row < m - 1 && visited[row + 1][col] != 1 && heights[row + 1][col] >= height) {
                pq.push({row + 1, col});
                visited[row + 1][col] = 1;
            }
        }
    }
    
    void atlanticBFS(int row, int col, vector<vector<int>>& heights, vector<vector<int>>& visited, vector<vector<int>>& ans) {
        
        int m = heights.size();
        int n = heights[0].size();

        if(visited[row][col] == 2) {
            return;
        }

        queue<pair<int, int>> pq;

        pq.push({row, col});
        if(visited[row][col] == 1) {
            ans.push_back({row, col});
        }
        visited[row][col] = 2;

        while(!pq.empty()) {

            pair current = pq.front(); pq.pop();

            int row = current.first;
            int col = current.second;
            int height = heights[row][col];

            // top
            if(row > 0 && visited[row - 1][col] != 2 && heights[row - 1][col] >= height) {
                pq.push({row - 1, col});
                if(visited[row - 1][col] == 1) {
                    ans.push_back({row - 1, col});
                }
                visited[row - 1][col] = 2;
            }

            // left
            if(col > 0 && visited[row][col - 1] != 2 && heights[row][col - 1] >= height) {
                pq.push({row, col - 1});
                if(visited[row][col - 1] == 1) {
                    ans.push_back({row, col - 1});
                }
                visited[row][col - 1] = 2;
            }

            // right
            if(col < n - 1 && visited[row][col + 1] != 2 && heights[row][col + 1] >= height) {
                pq.push({row, col + 1});
                if(visited[row][col + 1] == 1) {
                    ans.push_back({row, col + 1});
                }
                visited[row][col + 1] = 2;
            }

            // bottom
            if(row < m - 1 && visited[row + 1][col] != 2 && heights[row + 1][col] >= height) {
                pq.push({row + 1, col});
                if(visited[row + 1][col] == 1) {
                    ans.push_back({row + 1, col});
                }
                visited[row + 1][col] = 2;
            }
        }
    }

    vector<vector<int>> pacificAtlantic(vector<vector<int>>& heights) {
        
        int m = heights.size();
        int n = heights[0].size();
        
        vector<vector<int>> visited(m, vector<int>(n, 0));
        
        // reach of pacific Ocean
        // 1
        
        for(int i = 0; i < n; ++i) {
            pacificBFS(0, i, heights, visited);
        }
        for(int i = 1; i < m; ++i) {
            pacificBFS(i, 0, heights, visited);
        }

        // reach of Atlantic Ocean
        // if cell == 1, include in ans;
        // 2
        
        vector<vector<int>> ans;

        for(int i = 0; i < n; ++i) {
            atlanticBFS(m - 1, i, heights, visited, ans);
        }
        for(int i = 0; i < m; ++i) {
            atlanticBFS(i, n - 1, heights, visited, ans);
        }
        
        sort(ans.begin(), ans.end());

        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151136079-e44d5609-876a-40b7-bc86-32365b486420.png)](https://leetcode.com/submissions/detail/628151380/)
