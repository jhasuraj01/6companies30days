# Word Search

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/word-search/1/#)

Given a 2D board of letters and a word. Check if the word exists in the board. The word can be constructed from letters of adjacent cells only. ie - horizontal or vertical neighbors. The same letter cell can not be used more than once.

### Sample Input
```
1
3 4 
a g b c 
q e e l 
g b k s 
geeks
```
### Sample Output
```
1
```

### Solution
```cpp
class Solution {
public:

    bool findWord(int i, int j, int index, vector<vector<char>>& board, string& word, vector<vector<int>>& visited) {
        
        if(visited[i][j]) return false;
        if(index == word.size()) return true;
        
        visited[i][j] = 1;
        
        // up
        if(i > 0 && word[index] == board[i-1][j]) {
            if(findWord(i-1, j, index + 1, board, word, visited)) {
                return true;
            }
        }
        
        // down
        if(i < board.size()-1 && word[index] == board[i+1][j]) {
            if(findWord(i+1, j, index + 1, board, word, visited)) {
                return true;
            }
        }
        
        // left
        if(j > 0 && word[index] == board[i][j-1]) {
            if(findWord(i, j-1, index + 1, board, word, visited)) {
                return true;
            }
        }
        
        // right
        if(j < board[0].size()-1 && word[index] == board[i][j+1]) {
            if(findWord(i, j+1, index + 1, board, word, visited)) {
                return true;
            }
        }
        
        visited[i][j] = 0;
        
        return false;
    }

    bool isWordExist(vector<vector<char>>& board, string word) {
        
        int height = board.size();
        int width = board[0].size();
        
        vector<vector<int>> visited(height, vector<int>(width, 0));

        for(int i = 0; i < height; ++i) {
            for(int j = 0; j < width; ++j) {
                if(board[i][j] == word[0] && findWord(i, j, 1, board, word, visited)) {
                    return true;
                }
                
            }
        }
        
        return false;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/150655116-0700571c-d3b4-4767-9e10-2e7ae53b559e.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=67aa95b6421b99e7f44cd0805a9b512b&pid=702088&user=jhasuraj)
