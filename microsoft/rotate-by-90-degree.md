# Rotate by 90 degree

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/rotate-by-90-degree0356/1/#)

Given a square matrix[][] of size N x N. The task is to rotate it by 90 degrees in an anti-clockwise direction without using any extra space.

### Sample Input
```
5
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25
```
### Sample Output
```
5 10 15 20 25 
4 9 14 19 24 
3 8 13 18 23 
2 7 12 17 22 
1 6 11 16 21 
```

### Solution
```cpp
void rotate(int n,int a[][n])
{
    int limit = (n+1)/2;

    for(int r = 0; r < limit; ++r) {
        for(int c = r; c < n-r-1; ++c) {
            int temp = a[r][c];
            a[r][c] = a[c][n - r - 1];
            a[c][n - r - 1] = a[n - r - 1][n - c - 1];
            a[n - r - 1][n - c - 1] = a[n - c - 1][r];
            a[n - c - 1][r] = temp;
        }
    }
}
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149125771-8a440730-bffb-4f51-9428-3884f5cdb00c.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=0e64a2357d5660e471a3a6dbd4a922cc&pid=701989&user=jhasuraj)
