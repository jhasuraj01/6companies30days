# Number of Unique Paths

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/number-of-unique-paths5339/1/#)

Given a A X B matrix with your initial position at the top-left cell, find the number of possible unique paths to reach the bottom-right cell of the matrix from the initial position.

**Note:** Possible moves can be either down or right at any point in time, i.e., we can move to matrix[i+1][j] or matrix[i][j+1] from matrix[i][j].

### Sample Input
```
4 4
```

### Sample Output
```
20
```

### Solution
```cpp
class Solution
{
    public:
    int NumberOfPath(int a, int b)
    {
        vector<vector<int>> M(a, vector<int>(b, 1));
        
        for(int r = 1; r < a; ++r) {
            for(int c = 1; c < b; ++c) {
                M[r][c] = M[r-1][c] + M[r][c-1];
            }
        }

        return M.back().back();
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151651824-26986bcc-cd3c-4654-a870-b210a006d337.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=7bf1795b21916bac65f47e3dc374aa5a&pid=701714&user=jhasuraj)
