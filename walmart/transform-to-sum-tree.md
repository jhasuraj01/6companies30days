# Transform to Sum Tree 

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/transform-to-sum-tree/1/#)

Given a Binary Tree of size N , where each node can have positive or negative values. Convert this to a tree where each node contains the sum of the left and right sub trees of the original tree. The values of leaf nodes are changed to 0.

### Sample Input
```
         10
      /      \
    -2        6
   /   \     /  \
 8     -4   7    5
```

### Sample Output
```
        20
      /    \
    4        12
   /  \     /  \
 0     0   0    0
```

### Solution
```cpp
class Solution {
  public:
    int createSumTree(Node *node) {
        
        if(node == NULL) return 0;
        
        int left = createSumTree(node->left);
        int right = createSumTree(node->right);
        int temp = node->data;
        node->data = left + right;
        
        return (left + right + temp);
    }
    
    void toSumTree(Node *node)
    {
       createSumTree(node);
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151652298-1eb2b8cf-e159-4be4-8913-6a692b248ce4.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=203fa42114545239ef824c0dd52130df&pid=700185&user=jhasuraj)