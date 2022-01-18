# Winner of an election

[![Problem Link](../assets/gfg.svg)](...problem...)

Given an array of names (consisting of lowercase characters) of candidates in an election. A candidate name in array represents a vote casted to the candidate. Print the name of candidate that received Max votes. If there is tie, print lexicographically smaller name.

### Sample Input
```
13
john johnny jackie johnny john jackie jamie jamie john johnny jamie johnny john
```
### Sample Output
```
john 4
```

### Solution
```cpp
class Solution {
  public:
    vector<string> winner(string arr[],int n)
    {
        unordered_map<string, int> votes;

        for(int i = 0; i < n; ++i) {
            ++votes[arr[i]];
        }

        unordered_map<int, vector<string>> rank;

        int max_vote = 0;
        for(auto candidate: votes) {
            if(candidate.second >= max_vote) {
                max_vote = candidate.second;
                rank[max_vote].push_back(candidate.first);
            }
        }

        sort(rank[max_vote].begin(), rank[max_vote].end());

        return {rank[max_vote][0], to_string(max_vote)};
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149932325-1e2f8cd1-19e2-406f-8d41-593bc94b0e1f.png)](...solution...)
