# Minimum Swaps to Arrange a Binary Grid

[![Problem Link](../assets/lc.svg)](https://leetcode.com/problems/minimum-swaps-to-arrange-a-binary-grid/)

Given an n x n binary grid, in one step you can choose two adjacent rows of the grid and swap them.

A grid is said to be valid if all the cells above the main diagonal are zeros.

Return the minimum number of steps needed to make the grid valid, or -1 if the grid cannot be valid.

The main diagonal of a grid is the diagonal that starts at cell (1, 1) and ends at cell (n, n).

### Example 1
```
Input: grid = [[0,0,1],[1,1,0],[1,0,0]]
Output: 3
```

### Example 2
```
Input: grid = [[0,1,1,0],[0,1,1,0],[0,1,1,0],[0,1,1,0]]
Output: -1
```

### Solution
```cpp
class Solution {
public:
    int minSwaps(vector<vector<int>>& grid) {

        int side = grid.size();

        vector<int> suffix0(side);

        for(int i = 0; i < side; ++i) {
            int count = 0;
            while(count < side && grid[i][side - count - 1] == 0) ++count;
            suffix0[i] = count;
        }

        int count = 0;

        for(int i = 0; i < side; ++i) {
            int j = i;

            while(j < side && suffix0[j] < side - 1 - i) ++j;

            if(j == side) {
                return -1;
            }

            for(; j > i; --j) {
                swap(suffix0[j], suffix0[j - 1]);
                count++;
            }
        }

        return count;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151391127-75789eca-291a-46d0-b7d2-ad3513120677.png)](https://leetcode.com/submissions/detail/629008220/)