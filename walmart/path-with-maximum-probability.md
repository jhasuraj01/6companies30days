# Path with Maximum Probability

[![Problem Link](../assets/lc.svg)](https://leetcode.com/problems/path-with-maximum-probability/)

You are given an undirected weighted graph of n nodes (0-indexed), represented by an edge list where edges[i] = [a, b] is an undirected edge connecting the nodes a and b with a probability of success of traversing that edge succProb[i].

Given two nodes start and end, find the path with the maximum probability of success to go from start to end and return its success probability.

If there is no path from start to end, return 0. Your answer will be accepted if it differs from the correct answer by at most 1e-5.

### Example 1
```
Input: n = 3, edges = [[0,1],[1,2],[0,2]], succProb = [0.5,0.5,0.2], start = 0, end = 2
Output: 0.25000
```

### Example 2
```
Input: n = 3, edges = [[0,1],[1,2],[0,2]], succProb = [0.5,0.5,0.3], start = 0, end = 2
Output: 0.30000
```

### Solution
```cpp
class Solution {
public:
    double maxProbability(int n, vector<vector<int>>& edges, vector<double>& prob, int start, int end) {
        vector<bool> fixed(n, false);
        vector<double> ans(n, 0);
        ans[start] = 1;
        
        vector<vector<pair<double, int>>> graph(n);
        
        for(int i = 0; i < edges.size(); ++i) {
            graph[edges[i][0]].push_back({prob[i], edges[i][1]});
            graph[edges[i][1]].push_back({prob[i], edges[i][0]});
        }
        
        priority_queue<pair<double, int>> pq;
        
        pq.push({1.0, start});
        
        while(!pq.empty()) {
            pair<double, int> entry = pq.top(); pq.pop();
            
            double src_val = entry.first;
            int src_node = entry.second;

            if(!fixed[src_node]) {
                fixed[src_node] = true;
                
                for(auto dest: graph[src_node]) {
                    double probability = dest.first;
                    int dest_node = dest.second;
                    if(ans[dest_node] < src_val * probability) {
                        ans[dest_node] = src_val * probability;
                        pq.push({ans[dest_node], dest_node});
                    }
                }
            }
        }

        return ans[end];
    }
};
```

### Approach 2 (Error on Test Case 9)
```cpp
class Solution {
public:
    double maxProbability(int n, vector<vector<int>>& edges, vector<double>& succProb, int start, int end) {
        vector<pair<double, int>> prob(n);
        for(int i = 0; i < n; ++i) {
            prob[i].first = (double) 0.0;
            prob[i].second = i;
        }
        prob[start].first = (double) 1.0;

        // build matrix representation
        vector<vector<double>> graph(n, vector<double>(n , (double)0.0));

        for(int i = 0, limit = edges.size(); i < limit; ++i) {
            int a = edges[i][0];
            int b = edges[i][1];
            graph[a][b] = succProb[i];
            graph[b][a] = succProb[i];
        }

        auto swap_node = [&](int i, int j) {
            swap(prob[i], prob[j]);
        };

        swap_node(0, start);

        for(int src = 0; src < n - 1; ++src) {
            int max = src + 1;

            for(int des = src + 1; des < n; ++des) {
                int pos_src = prob[src].second;
                int pos_des = prob[des].second;

                double val_des = prob[des].first;
                double val_src = prob[src].first;
                double probability = graph[pos_src][pos_des];

                if(val_des < val_src * probability) {
                    prob[des].first = val_src * probability;
                    if(prob[max].first < prob[des].first) max = des;
                }
            }
            if(prob[max].second == end) {
                return prob[max].first;
            }
            swap_node(max, src + 1);
        }

        return 0;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151697012-4f8dbce0-ba12-442f-96b2-c28149baa984.png)](https://leetcode.com/submissions/detail/630872979/)
