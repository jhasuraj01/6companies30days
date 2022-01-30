# Find Array Given Subset Sums

[![Problem Link](../assets/lc.svg)](https://leetcode.com/problems/find-array-given-subset-sums/)

You are given an integer n representing the length of an unknown array that you are trying to recover. You are also given an array sums containing the values of all 2n subset sums of the unknown array (in no particular order).

Return the array ans of length n representing the unknown array. If multiple answers exist, return any of them.

An array sub is a subset of an array arr if sub can be obtained from arr by deleting some (possibly zero or all) elements of arr. The sum of the elements in sub is one possible subset sum of arr. The sum of an empty array is considered to be 0.

**Note:** Test cases are generated such that there will always be at least one correct answer.

### Example 1
```
Input: n = 3, sums = [-3,-2,-1,0,0,1,2,3]
Output: [1,2,-3]
```

### Example 2
```
Input: n = 2, sums = [0,0,0,0]
Output: [0,0]
```

### Solution
```cpp
class Solution {
public:
    void print(vector<int> &v) {
        for(auto &e: v) {
            cout << e << " ";
        }
        cout << endl;
    }
    vector<int> array(int n, vector<int>& sums) {
        if(n == 1) {
            vector<int> result;
            if(sums[0] == 0) {
                result.push_back(sums[1]);
            }
            else if(sums[1] == 0) {
                result.push_back(sums[0]);
            }
            return result;
        }

        int num = sums[(1 << n) - 1] - sums[(1 << n) - 2];

        unordered_map<int, int> freq1;
        unordered_map<int, int> freq2;
        for(int sum: sums) {
            ++freq1[sum];
            ++freq2[sum];
        }

        // cosider num = |largest negative num|
        vector<int> neg;
        bool valid_neg = false;
        for(auto sum: sums) {
            if(freq1.count(sum) && freq1.count(sum + num)) {
                if(freq1[sum] > 0) {
                    neg.push_back(sum + num);
                    if(sum + num == 0) valid_neg = true;
                    --freq1[sum];
                    --freq1[sum + num];
                }
            }
            else {
                if(freq1[sum] > 0)
                    break;
            }
        }

        if(valid_neg && neg.size() == (1 << (n - 1))) {
            vector<int> result = array(n - 1, neg);
            result.push_back(-num);
            if(result.size() == n) 
                return result;
        }
        
        // cosider num = |smallest positive num|
        vector<int> pos;
        bool valid_pos = false;
        int limit = (1 << n);
        for(int i = 0; i < limit; ++i) {
            int sum = sums[limit - 1 - i];
            if(freq2.count(sum) && freq2.count(sum - num)) {
                if(freq2[sum] > 0) {
                    pos.push_back(sum - num);
                    if(sum - num == 0) valid_pos = true;
                    --freq2[sum];
                    --freq2[sum - num];
                }
            }
            else {
                if(freq2[sum] > 0)
                    break;
            }
        }

        if(valid_pos && pos.size() == (1 << (n - 1))) {
            reverse(pos.begin(), pos.end());
            vector<int> result = array(n - 1, pos);
            result.push_back(num);
            if(result.size() == n) 
                return result;
        }

        return vector<int>(0);
    }

    vector<int> recoverArray(int n, vector<int>& sums) {
        sort(sums.begin(), sums.end());
        return array(n, sums);
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151711042-c36f4cb0-f57a-44f7-b032-f0a786d05701.png)](https://leetcode.com/submissions/detail/631059018/)