# Minimum operations to convert array A to B

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/minimum-insertions-to-make-two-arrays-equal/1/#)

Given two Arrays **A[]** and **B[]** of length **N** and **M** respectively. Find the minimum number of **insertions** and **deletions** on the array A[], required to make both the arrays identical.

**Note:** Array B[] is sorted and all its elements are distinct, operations can be performed at any index not necessarily at end.

### Sample Input
```
1
5 3
1 2 5 3 1
1 3 5
```

### Sample Output
```
4
```

### 2D - DP (Memory Limit Exceeded)
```cpp
class Solution {
  public:
    int minEditDistance(int A[], int B[], int& N, int& M, int a, int b, vector<vector<int>> &cache) {
        if(a == N) return M - b;
        if(b == M) return N - a;
        if(cache[a][b] != -1) return cache[a][b];

        if(A[a] == B[b]) {
            return cache[a][b] = minEditDistance(A, B, N, M, a+1, b+1, cache);
        }
        else {
            return cache[a][b] = min({
                minEditDistance(A, B, N, M, a+1, b, cache) + 1,
                minEditDistance(A, B, N, M, a, b+1, cache) + 1,
                minEditDistance(A, B, N, M, a+1, b+1, cache) + 2
            });
        }
    }

    int minInsAndDel(int A[], int B[], int N, int M) {
        vector<vector<int>> cache(N+1, vector<int>(M+1, -1));
        return minEditDistance(A, B, N, M, 0, 0, cache);
    }
};
```

<!-- ### Accepted -->
<!-- [![image](...image...)](...solution...) -->
