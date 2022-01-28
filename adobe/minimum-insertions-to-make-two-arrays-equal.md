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

### Solution
```cpp
class Solution {
  public:
    int lengthOfLIS(vector<int>& nums) {
        if(nums.size() == 0) return 0;

        vector<int> seq;
        seq.push_back(nums[0]);

        for(int i = 1; i < nums.size(); ++i) {
            if(seq.back() < nums[i]) {
                seq.push_back(nums[i]);
                continue;
            }
            int index = lower_bound(seq.begin(), seq.end(), nums[i]) - seq.begin();
            seq[index] = nums[i];
        }
        return seq.size();
    }

    int minInsAndDel(int A[], int B[], int N, int M) {
        vector<int> MA;
        bitset<100001> availabe;
        
        for(int i = 0; i < M; ++i) {
            availabe.set(B[i]);
        }

        for(int i = 0; i < N; ++i) {
            if(availabe[A[i]]) {
                MA.push_back(A[i]);
            }
        }
        int lis = lengthOfLIS(MA);
        return (N + M - lis*2);
    }
};
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

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151556401-7a5e02bb-6c1d-4f89-bb79-59220688ee40.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=9bf4ff89ca1f88a081a9b24e346f47d6&pid=706334&user=jhasuraj)
