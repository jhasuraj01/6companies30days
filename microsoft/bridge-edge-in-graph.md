# Bridge edge in a graph

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/bridge-edge-in-graph/1#)

Given a Graph of V vertices and E edges and another edge(c - d), the task is to find if the given edge is a Bridge. i.e., removing the edge disconnects the graph.

### Sample Input
```
4 4
0 1
1 2
2 3
1 3
1 2
```
### Sample Output
```
0
```

### Solution
```cpp
class Solution {
	public:
    int isBridge(int V, vector<int> adj[], int c, int d) 
    {
        vector<bool> q1ed(V, false), q2ed(V, false);
        queue<int> q1, q2;

        q1.push(c);
        q1ed[c] = true;

        q2.push(d);
        q2ed[d] = true;

        while(!q1.empty() && !q2.empty()) {
            int cReached = q1.front(); q1.pop();
            int dReached = q2.front(); q2.pop();

            if(q2ed[cReached] || q1ed[dReached]) {
                return 0;
            }

            for(auto node: adj[cReached]) {
                if(q1ed[node] || (cReached == c && node == d)) continue;
                q1.push(node);
                q1ed[node] = true;
            }

            for(auto node: adj[dReached]) {
                if(q2ed[node] || (dReached == d && node == c)) continue;
                q2.push(node);
                q2ed[node] = true;
            }
        }
        return 1;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149377980-4c504861-d45a-4a66-8b0e-91407a61fb1d.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=67a1531e0d0963e0b9e76b42c46ea177&pid=700463&user=jhasuraj)
