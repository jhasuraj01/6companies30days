# Array Pair Sum Divisibility Problem

[![Problem Link](https://img.shields.io/badge/GeeksforGeeks-298D46?style=for-the-badge&logo=geeksforgeeks&logoColor=white)](https://practice.geeksforgeeks.org/problems/array-pair-sum-divisibility-problem3257/1#)


### Sample Input
```
4 6
9 7 5 3
```

### Sample Output
```
True
```

### Solution
```cpp
class Solution {
  public:
    bool canPair(vector<int> nums, int k) {

        if(nums.size() % 2) return false;

        unordered_map<int, int> rem;

        for(int n: nums) {
            int r = n%k;

            if(r && rem.count(k - r) && rem[k - r] > 0) {
                --rem[k - r];
                rem[0] += 2;
            }
            else {
                ++rem[r];
            }
        }
    
        return rem[0] == nums.size();
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/147900297-3ee0968e-7bb6-476b-865c-0fcb3d6d856d.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=44e5a1b367208553109b112ee8da26e2&pid=704691&user=jhasuraj)
