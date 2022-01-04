# Squares in N*N Chessboard

[![Problem Link](https://img.shields.io/badge/GeeksforGeeks-298D46?style=for-the-badge&logo=geeksforgeeks&logoColor=white)](https://practice.geeksforgeeks.org/problems/squares-in-nn-chessboard1801/1#)

Find total number of Squares in a N*N chessboard.

### Calculation

let $f\left(n-1\right)$ and $f\left(n\right)$ be the number of squares in $\left(N-1\right)\cdot\left(N-1\right)$ and $N\cdot N$ chessboard respectively.

$\therefore f\left(n\right)=k+f\left(n-1\right)$

where, $k$ is increment in number of squares from $\left(N-1\right)\cdot\left(N-1\right)$ to $N\cdot N$ chessboard

> Hints for calculating $k$.
> 
> $k=\frac{n\cdot\left(n+1\right)}{2}+\frac{n\cdot\left(n+1\right)}{2}-n=n^{2}$

$\therefore f\left(n\right)\ =\ n^{2}+f\left(n-1\right)$

$\therefore f\left(n\right)\ =\ n^{2}+\left(n-1\right)^{2}+\left(n-2\right)^{2}+\cdot\cdot\cdot\ +\ 2^{2}+1^{2}+0^{2}$

$\therefore f\left(n\right)\ =\frac{n\cdot\left(n+1\right)\cdot\left(2n+1\right)}{6}$


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
