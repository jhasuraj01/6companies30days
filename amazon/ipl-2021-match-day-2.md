# IPL 2021 - Match Day 2

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/deee0e8cf9910e7219f663c18d6d640ea0b87f87/1/#)

Due to the rise of covid-19 cases in India, this year BCCI decided to organize knock-out matches in IPL rather than a league.

Today is matchday 2 and it is between the most loved team Chennai Super Kings and the most underrated team - Punjab Kings. Stephen Fleming, the head coach of CSK, analyzing the batting stats of Punjab. He has stats of runs scored by all N players in the previous season and he wants to find the maximum score for each and every contiguous sub-list of size K to strategize for the game.

### Sample Input
```
9 3
1 2 3 1 4 5 2 3 6
```
### Sample Output
```
3 3 4 5 5 5 6 
```

### Solution
```cpp
class Solution {
  public:
    vector<int> max_of_subarrays(vector<int> arr, int n, int k) {

        priority_queue<pair<int, int>> MAXQ;

        for(int i = 0; i < k; ++i) {
            MAXQ.push({arr[i], i});
        }
        
        vector<int>ans;
        ans.push_back(MAXQ.top().first);

        for(int i = k; i < n; ++i) {
            MAXQ.push({arr[i], i});
            
            while(!MAXQ.empty() && MAXQ.top().second <= i - k) {
                MAXQ.pop();
            }
            
            ans.push_back(MAXQ.top().first);
        }
        
        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148422429-9b5e7888-36a7-423a-99ae-5a0fd7319843.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=d0ce9ea64d23cd3d9ea701d62d76a039&pid=707042&user=jhasuraj)
