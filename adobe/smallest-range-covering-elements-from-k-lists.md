# Smallest range in K lists

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/find-smallest-range-containing-elements-from-k-lists/1/#)

Given K sorted lists of integers, KSortedArray[] of size N each. The task is to find the smallest range that includes at least one element from each of the K lists. If more than one such range's are found, return the first such range found.

### Sample Input
```
5 3
1 3 5 7 9
0 2 4 6 8
2 3 5 7 11
```

### Sample Output
```
1 2
```

### Solution
```cpp
#define pipi pair<int, pair<int, int>>
class Solution {
    public:
    pair<int,int> findSmallestRange(int KSortedArray[][N], int n, int k)
    {
        priority_queue<pipi, vector<pipi>, greater<pipi>> minheap;
        
        int low = INT_MAX, high = INT_MIN;
        for(int i = 0; i < k; ++i) {
            int val = KSortedArray[i][0];
            low = min(low, val);
            high = max(high, val);
            minheap.push({val, {i, 0} });
        }

        int range = high - low;
        int max_value = high;
        int min_value = low;

        while(true) {
            pipi min_entry = minheap.top(); minheap.pop();

            int new_row = min_entry.second.first;
            int new_col = min_entry.second.second + 1;
            if(new_col >= n) break;

            int new_val = KSortedArray[new_row][new_col];
            minheap.push({new_val, {new_row, new_col}});

            min_value = minheap.top().first;
            max_value = max(max_value, new_val);

            if(max_value - min_value < range) {
                low = min_value;
                high = max_value;
                range = high - low;
            }
        }

        return {low, high};
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151532286-0062f227-fa57-4756-ba11-d5435988cece.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=b0ca0e6990a7903142a197b365a7a265&pid=700497&user=jhasuraj)
