# Find All Four Sum Numbers

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/find-all-four-sum-numbers1732/1#)

Given an array of integers and another number. Find all the unique quadruple from the given array that sums up to the given number.

### Sample Input
```
5 3
0 0 2 1 1 
```
### Sample Output
```
0 0 1 2 $
```

### Solution
```cpp
class Solution {
    public:
    vector<vector<int> > fourSum(vector<int> &arr, int k) {

        unordered_set<string> collection;
        
        sort(arr.begin(), arr.end());

        int n = arr.size();

        vector<vector<int>> ans;

        for(int i = 0; i < n; ++i) {
            for(int j = i+1; j < n; ++j) {

                int l = 0;
                int r = n-1;

                while(l < r) {
                    if(l == i || l == j) {
                        ++l;
                        continue;
                    }
                    if(r == i || r == j) {
                        --r;
                        continue;
                    }

                    int sum = arr[i] + arr[j] + arr[l] + arr[r];

                    if(sum == k) {

                        vector<int> quadruple = {arr[i], arr[j], arr[l], arr[r]};
                        sort(quadruple.begin(), quadruple.end());
                        
                        string hash = "";
                        for(int num: quadruple) {
                            hash += to_string(num) + ':';
                        }

                        if(collection.count(hash) == 0) {
                            ans.push_back(quadruple);
                            collection.insert(hash);
                        }

                        ++l;
                        --r;
                    }
                    else if(sum < k) {
                        ++l;
                    }
                    else if(sum > k) {
                        --r;
                    }
                }
            }
        }
        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149371234-a8ddee7a-88d5-49dc-bb93-40da757a1acc.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=f27efa8ecab118e23f5489f5a9e4c1bf&pid=702139&user=jhasuraj)
