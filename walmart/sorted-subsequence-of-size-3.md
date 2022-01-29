# Sorted subsequence of size 3

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/sorted-subsequence-of-size-3/1/#)

Given an array A of N integers, find any 3 elements in it such that A[i] < A[j] < A[k] and i < j < k.

### Sample Input
```
5
1 2 1 1 3
```
### Sample Output
```
1 2 3
```

### Solution
```cpp
class Solution {
  public:
    vector<int> find3Numbers(vector<int> nums, int N) {
        int len = 1;
        vector<int> seq(3, INT_MAX), pos(3, -1), mapping(N, -1);
        seq[0] = nums[0];
        pos[0] = 0;

        for(int i = 1; i < N && len < 3; ++i) {
            int index;

            if(seq[len - 1] < nums[i]) {
                index = len;
                len++;
            }
            else {
                index = lower_bound(seq.begin(), seq.end(), nums[i]) - seq.begin();
            }

            seq[index] = nums[i];
            pos[index] = i;

            if(index > 0) {
                mapping[i] = pos[index - 1];
            }
        }

        if(len < 3) return vector<int>(0);

        vector<int> result(3, 0);
        int ptr = pos[2];
        for(int i = 0; i < 3; ++i) {
            result[2-i] = nums[ptr];
            ptr = mapping[ptr];
        }

        return result;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151654579-91e14de3-3f47-4ce0-881b-2a9de4fa265f.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=dae1ec7de9ef9800f03ed13ac19ab231&pid=700357&user=jhasuraj)