# Alien Dictionary

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/alien-dictionary/1/#)

Given a sorted dictionary of an alien language having N words and k starting alphabets of standard dictionary. Find the order of characters in the alien language.

**Note:** Many orders may be possible for a particular test case, thus you may return any valid order and output will be 1 if the order of string returned by the function is correct else 0 denoting incorrect string returned.

### Sample Input
```
6 3
cb ca bb ba ab aa
```
### Sample Output
```
cba
```

### Solution
```cpp
class Solution {
    public:
    string topologicalSort(char parent, unordered_map<char, vector<char>> &G, unordered_set<char> &visited) {
        if(visited.count(parent)) return "";

        visited.insert(parent);

        if(G.count(parent) == 0) return string(1, parent);

        string ans = "";
        for(auto child: G[parent]) {
            ans += topologicalSort(child, G, visited);
        }

        ans += parent;

        return ans;
    }

    string findOrder(string dict[], int N, int K) {

        unordered_map<char, vector<char>> G;

        // build graph
        for(int i = 1; i < N; ++i) {
            int j = 0;
            int limit = min(dict[i-1].size(), dict[i].size());

            while(j < limit && dict[i-1][j] == dict[i][j]) ++j;

            if(j < limit) G[dict[i-1][j]].push_back(dict[i][j]);
        }

        unordered_set<char> visited;
        string ans_rev = "";

        for(auto node: G) {
            if(visited.count(node.first)) continue;
            ans_rev += topologicalSort(node.first, G, visited);
        }

        reverse(ans_rev.begin(), ans_rev.end());

        return ans_rev;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149466291-7824cfff-f319-4d5c-8b0c-c1ee69eb51fc.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=7ba812bc35c449816be4f5152be73b3b&pid=700494&user=jhasuraj)
