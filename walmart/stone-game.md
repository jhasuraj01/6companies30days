# Stone Game

[![Problem Link](../assets/lc.svg)](link)

Alice and Bob play a game with piles of stones. There are an even number of piles arranged in a row, and each pile has a positive integer number of stones piles[i].

The objective of the game is to end with the most stones. The total number of stones across all the piles is odd, so there are no ties.

Alice and Bob take turns, with Alice starting first. Each turn, a player takes the entire pile of stones either from the beginning or from the end of the row. This continues until there are no more piles left, at which point the person with the most stones wins.

Assuming Alice and Bob play optimally, return true if Alice wins the game, or false if Bob wins.

### Example 1
```
Input: piles = [5,3,4,5]
Output: true
```

### Example 2
```
Input: piles = [3,7,2,3]
Output: true
```

### Solution
```cpp
class Solution {
public:
    int maxStone(vector<int>&A,int n, int start, int end, vector<vector<int>>& cache) {
        
        if(end < start) {
            return 0;
        }
        if(end == start) {
            return A[end];
        }
        if(cache[start][end] != -1) return cache[start][end];
        
        return cache[start][end] = max({
            A[start] + min(maxStone(A, n, start + 2, end, cache), maxStone(A, n, start + 1, end - 1, cache)),
            A[end]   + min(maxStone(A, n, start, end - 2, cache), maxStone(A, n, start + 1, end - 1, cache))
        });
    }

    bool stoneGame(vector<int>& piles) {
        int n = piles.size();
        vector<vector<int>> cache(n, vector<int>(n, -1));
	    int alice = maxStone(piles, n, 0, n-1, cache);
        int bob = accumulate(piles.begin(), piles.end(), 0) - alice;

        return alice > bob;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151697563-1041ec14-49ab-4efd-bbb9-74b7ffc221b9.png)](https://leetcode.com/submissions/detail/630880110/)