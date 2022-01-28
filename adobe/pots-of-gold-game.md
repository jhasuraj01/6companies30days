# Pots of Gold Game

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/pots-of-gold-game/1/#)

Two players X and Y are playing a game in which there are pots of gold arranged in a line, each containing some gold coins. They get alternating turns in which the player can pick a pot from one of the ends of the line. The winner is the player who has a higher number of coins at the end. The objective is to maximize the number of coins collected by X, assuming Y also plays optimally.

Return the maximum coins X could get while playing the game. Initially, X starts the game.

### Sample Input
```
4
8 15 3 7
```

### Sample Output
```
22
```

### Solution
```cpp
class Solution {
public:
    int maxCoins(vector<int>&A,int n, int start, int end, vector<vector<int>>& cache) {
        
        if(end < start) {
            return 0;
        }
        if(end == start) {
            return A[end];
        }
        if(cache[start][end] != -1) return cache[start][end];
        
        return cache[start][end] = max({
            A[start] + min(maxCoins(A, n, start + 2, end, cache), maxCoins(A, n, start + 1, end - 1, cache)),
            A[end]   + min(maxCoins(A, n, start, end - 2, cache), maxCoins(A, n, start + 1, end - 1, cache))
        });
    }
    int maxCoins(vector<int>&A,int n)
    {
        vector<vector<int>> cache(n, vector<int>(n, -1));
	    return maxCoins(A, n, 0, n-1, cache);
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151496293-50c4ee77-9b59-42ab-9f61-d4a536500697.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=9e35a87b0b5f934277144b50627eeaec&pid=700428&user=jhasuraj)
