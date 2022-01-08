# Is Sudoku Valid

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/is-sudoku-valid4820/1/#)

Given an incomplete Sudoku configuration in terms of a 9x9  2-D square matrix(mat[][]) the task to check if the current configuration is valid or not where a 0 represents an empty block.

**Note:** Current valid configuration does not ensure validity of the final solved sudoku.

Refer to this : https://en.wikipedia.org/wiki/Sudoku

### Sample Input
```
3 0 6 5 0 8 4 0 0 
5 2 0 0 0 0 0 0 0 
0 8 7 0 0 0 0 3 1 
0 0 3 0 1 0 0 8 0 
9 0 0 8 6 3 0 0 5 
0 5 0 0 9 0 6 0 0 
1 3 0 0 0 0 2 5 0 
0 0 0 0 0 0 0 7 4 
0 0 5 2 0 6 3 0 0
```
### Sample Output
```
1
```

### Solution
```cpp
class Solution{
public:
    int isValid(vector<vector<int>> mat){

        // row, col, block cache
        vector<bitset<10>> rowc(9), colc(9), bloc(9);

        for(int r = 0; r < 9; ++r) {
            for(int c = 0; c < 9; ++c) {
                int num = mat[r][c];
                
                if(
                    num && (
                    rowc[r].test(num) ||
                    colc[c].test(num) ||
                    bloc[3*(r/3) + c/3].test(num))
                ) return 0;
                
                rowc[r].set(num);
                colc[c].set(num);
                bloc[3*(r/3) + c/3].set(num);
            }
            
        }
        return 1;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148640951-447e634c-e890-4c85-9f7a-dc1ef99c5893.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=066bfa3e462dabebf51f08ab533006ec&pid=705293&user=jhasuraj)
