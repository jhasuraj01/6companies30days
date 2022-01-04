# Squares in N*N Chessboard

[![Problem Link](https://img.shields.io/badge/GeeksforGeeks-298D46?style=for-the-badge&logo=geeksforgeeks&logoColor=white)](https://practice.geeksforgeeks.org/problems/squares-in-nn-chessboard1801/1#)

Find total number of Squares in a N*N chessboard.

### Calculation
![image](https://user-images.githubusercontent.com/44930179/148076998-47c3228c-51de-440d-bb2b-d5e93bc087ed.png)


### Sample Input
```
2
```
### Sample Output
```
5
```

### Solution
```cpp
class Solution {
  public:
    long long squaresInChessBoard(long long N) {
        
        long long ans = N * (N + 1) * (2*N + 1) / 6;
        
        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148070469-fbeadb72-174e-4429-84d3-a58fae2cb63e.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=fa05c17a6461f5dbc7ff804201c6020d&pid=704775&user=jhasuraj)
