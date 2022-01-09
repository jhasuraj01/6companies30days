# Brackets in Matrix Chain Multiplication

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/brackets-in-matrix-chain-multiplication1024/1/#)

Given an array p[] of length n used to denote the dimensions of a series of matrices such that dimension of i'th matrix is p[i] * p[i+1]. There are a total of n-1 matrices. Find the most efficient way to multiply these matrices together. 
The problem is not actually to perform the multiplications, but merely to decide in which order to perform the multiplications such that you need to perform minimum number of multiplications. There are many options to multiply a chain of matrices because matrix multiplication is associative i.e. no matter how one parenthesize the product, the result will be the same.

### Sample Input
```
5
1 2 3 4 5
```
### Sample Output
```
(((AB)C)D)
```

### Solution
```cpp
#define pis pair<int, string> 

class Solution{
public:
    string matrixChainOrder(int A[], int n){
        
        vector<vector<pis>> DP(n-1, vector<pis>(n-1));

        for(int i = 0; i < n-1; ++i) {
            string M = "";
            M += (char) ('A' + i);
            DP[i][i] = { 0, M };
        }
        

        for(int size = 1; size <= n; ++size) {
            int l = 0;
            int m = size;

            while(m < n-1) {

                DP[l][m].first = numeric_limits<int>::max();
    
                for(int i = l; i < m; ++i) {
                    int operations = DP[l][i].first + DP[i+1][m].first + A[l]*A[i+1]*A[m+1];

                    if(DP[l][m].first > operations) {
                        DP[l][m].second = "(" + DP[l][i].second + DP[i+1][m].second + ")";
                        DP[l][m].first = operations;
                    }
                    
                }

                ++l;
                ++m;
            }
        }

        return DP[0].back().second;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148676012-b102b552-c60c-4f07-aa12-05d904b16691.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=9b85d4c8a879148be735610bcf007721&pid=705397&user=jhasuraj)
