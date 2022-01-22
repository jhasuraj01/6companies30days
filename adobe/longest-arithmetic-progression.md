# Longest Arithmetic Progression

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/longest-arithmetic-progression1019/1/#)

Given an array called A[] of sorted integers having no duplicates, find the length of the Longest Arithmetic Progression (LLAP) in it.

### Sample Input
```
6
1 7 10 13 14 19
```

### Sample Output
```
4
```

### Solution
```cpp
class Solution {   
public:
    int lengthOfLongestAP(int A[], int n) {
        
        if(n == 1) return 1;
        if(n == 2) return 2;

        int ans = 2;

        vector<vector<int>> dp(n, vector<int>(n, 2));
        
        for(int x = n - 2; x > 0; --x) {
            int i = x - 1;
            int j = x + 1;
            
            while(i >= 0 && j < n) {
                if(A[i] + A[j] == 2 * A[x]) {
                    dp[i][x] = dp[x][j] + 1;
                    ans = max(ans, dp[i][x]);
                    --i;
                    ++j;
                }
                else if(A[i] + A[j] < 2 * A[x]) {
                    ++j;
                }
                else {
                    --i;
                }
            }
        }

        return ans;
    }
};
```
### Knapsack (TLE)
```cpp
class Solution {   
public:
    int AP_SIZE(int A[], int n, bitset<1000> selection) {
        
        int last_num, dif, size = 0;

        for(int i = 0; i < n; ++i) {
            if(size == 0 && selection[i]) {
                ++size;
                last_num = A[i];
            }
            else if(size == 1 && selection[i]) {
                ++size;
                dif = A[i] - last_num;
                last_num = A[i];
            }
            else if(size > 1 && selection[i]) {
                if(dif == A[i] - last_num) {
                    ++size;
                    dif = A[i] - last_num;
                    last_num = A[i];
                }
                else {
                    return 0;
                }
            }
        }
        return size;
    }

    int max_size(int A[], int n, int i, bitset<1000> selection, vector<unordered_map<bitset<1000>, int>>& cache) {

        if(i >= n) {
            return AP_SIZE(A, n, selection);
        }
        if(cache[i].count(selection)) return cache[i][selection];

        bitset<1000> new_selection = selection;
        new_selection[i] = 1;

        return cache[i][selection] = max(max_size(A, n, i + 1, selection, cache), max_size(A, n, i + 1, new_selection, cache));
    }

    int lengthOfLongestAP(int A[], int n) {
        bitset<1000> selection(0);
        vector<unordered_map<bitset<1000>, int>> cache(1000);
        return max_size(A, n, 0, selection, cache);
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/150653163-75f4c91d-a173-484a-a0ff-b542e6855752.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=92ef52d252cd3e098d536a2ff94977fb&pid=703290&user=jhasuraj)