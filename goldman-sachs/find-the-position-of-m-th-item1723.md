# Find the position of M-th item

[![Problem Link](https://img.shields.io/badge/GeeksforGeeks-298D46?style=for-the-badge&logo=geeksforgeeks&logoColor=white)](https://practice.geeksforgeeks.org/problems/find-the-position-of-m-th-item1723/1#)

M items are to be delivered in a circle of size N. Find the position where the M-th item will be delivered if we start from a given position K. Note that items are distributed at adjacent positions starting from K.

### Sample Input
```
5 8 2
```
### Sample Output
```
4
```

### Solution
```cpp
class Solution {
  public:
    int findPosition(int N , int M , int K) {
        if(N == 1) return 1;

        int pos = 1 + (M + K - 2) % N;
        return pos;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148000925-4b92ec5d-eae4-4e4f-a0c5-a90b532c2103.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=5caae207066adc0ddc8d191f13e6b1ce&pid=704216&user=jhasuraj)
