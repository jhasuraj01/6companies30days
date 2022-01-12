# Spirally traversing a matrix

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/spirally-traversing-a-matrix-1587115621/1/#)

Given a matrix of size r*c. Traverse the matrix in spiral form.

### Sample Input
```
4 4
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16
```
### Sample Output
```
1 2 3 4 8 12 16 15 14 13 9 5 6 7 11 10 
```

### Solution
```cpp
class Solution {   
    public: 
    vector<int> spirallyTraverse(vector<vector<int> > M, int r, int c) {
        int limit = r*c;
        vector<int> ans(limit);
        
        int x = 0, y = 0, dx = 1, dy = 0, boundary = 0;
        int index = 0;
        
        while(index < limit) {
            ans[index++] = M[y][x];

            if(dx == 1 && x == c - boundary - 1) {
                dx = 0;
                dy = 1;
            }

            if(dy == 1 && y == r - boundary - 1) {
                dx = -1;
                dy = 0;
            }

            if(dx == -1 && x == boundary) {
                dx = 0;
                dy = -1;
            }

            if(dy == -1 && y == boundary + 1) {
                dx = 1;
                dy = 0;
                ++boundary;
            }

            x += dx;
            y += dy;
        }
        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149137665-45bed8ef-ba3c-4c67-a132-ed00567c966b.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=810da18db6144f1c05684e662e7662e0&pid=701264&user=jhasuraj)
