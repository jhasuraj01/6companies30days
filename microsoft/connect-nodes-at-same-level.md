# Connect Nodes at Same Level

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/connect-nodes-at-same-level/1/#)

Given a binary tree, connect the nodes that are at same level. You'll be given an addition nextRight pointer for the same.

Initially, all the nextRight pointers point to garbage values. Your function should set these pointers to point next right for each node.
```
       10             10-->NULL
      / \            / \      
     3   5    =>    3-->5-->NULL
    / \   \        / \   \    
   4   1   2      4-->1-->2-->NULL
```
### Sample Input
```
3 1 2
```
### Sample Output
```
3 1 2 
1 3 2 
```

### Solution
```cpp
class Solution {
    public:
    void connect(Node *root)
    {
        queue<Node*> q;
        q.push(root);
        q.push(NULL);
        
        while(!q.empty()) {
            Node* node = q.front();
            q.pop();
    
            if(node == NULL) {
                if(!q.empty()) {
                    q.push(NULL);
                }
                continue;
            }
            
            node->nextRight = q.front();

            if(node->left) q.push(node->left);
            if(node->right) q.push(node->right);
        }
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149304947-65e87f00-8fcf-4d81-91a9-0fd4e00b939d.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=5dc3c130ce28f3d5b9fd088b625d5281&pid=700184&user=jhasuraj)
