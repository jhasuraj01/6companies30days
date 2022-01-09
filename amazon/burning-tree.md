# Burning Tree

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/burning-tree/1/#)

Given a binary tree and a node called target. Find the minimum time required to burn the complete binary tree if the target is set on fire. It is known that in 1 second all nodes connected to a given node get burned. That is its left child, right child, and parent.

### Sample Input
```
1 2 3 4 5 N 6 N N 7 8 N 9 N N N N N 10
8
```
### Sample Output
```
7
```

### Solution
```cpp
class Solution {
  public:
    int minTime(Node* root, int target) 
    {
        unordered_map<Node*, Node*> parent;

        //find target
        queue<Node*> q1;
        q1.push(root);

        Node* node;

        while(!q1.empty()) {
            node = q1.front();
            q1.pop();
            
            if(node->data == target) {
                break;
            }

            if(node->left != NULL) {
                parent[node->left] = node;
                q1.push(node->left);
            }

            if(node->right != NULL) {
                parent[node->right] = node;
                q1.push(node->right);
            }
        }

        // find largest dist
        queue<Node*> q2;
        q2.push(node);
        q2.push(NULL);

        unordered_map<Node*, bool> queued;
        int dist = -1;

        while(!q2.empty()) {

            node = q2.front();
            q2.pop();

            if(node == NULL) {
                ++dist;
                if(!q2.empty()) {
                    q2.push(NULL);
                }
                continue;
            }

            if(node->left != NULL && !queued.count(node->left)) {
                q2.push(node->left);
                queued[node->left] = true;
            }

            if(node->right != NULL && !queued.count(node->right)) {
                q2.push(node->right);
                queued[node->right] = true;
            }

            if(parent.count(node) && !queued.count(parent[node])) {
                q2.push(parent[node]);
                queued[parent[node]] = true;
            }
        }

        return dist;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148680071-cb6eb1ba-f7ea-4ceb-938b-2db5e0b00281.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=27145b0cafb4eebc74d3d7c237f48942&pid=702131&user=jhasuraj)
