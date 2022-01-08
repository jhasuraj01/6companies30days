# Serialize and Deserialize a Binary Tree

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/serialize-and-deserialize-a-binary-tree/1#)

Serialization is to store a tree in an array so that it can be later restored and Deserialization is reading tree back from the array. Now your task is to complete the function serialize which stores the tree into an array A[ ] and deSerialize which deserializes the array to the tree and returns it.

**Note:** The structure of the tree must be maintained. Multiple nodes can have the same data.

### Sample Input
```
1 2 3
```
### Sample Output
```
2 1 3
```

### Solution
```cpp
class Solution
{
    public:
    vector<int> serialize(Node *root) 
    {
        if(root == NULL) {
            return {};
        }

        vector<int> left = serialize(root->left);
        vector<int> right = serialize(root->right);

        vector<int> ans;

        // preallocate memory
        ans.reserve(left.size() + right.size() + 1);
        ans.insert(ans.end(), left.begin(), left.end());
        ans.push_back(root->data);
        ans.insert(ans.end(), right.begin(), right.end());

        return ans;
    }

    Node * deSerialize(vector<int> &A)
    {
        int N = A.size();

        if(N == 1) {
            Node* root = new Node(A[0]);
            return root;
        }
        if(N == 2) {
            Node* left = new Node(A[0]);
            Node* root = new Node(A[1]);
            root->left = left;
            return root;
        }

        Node* left = new Node(A[0]);
        Node* root = new Node(A[1]);
        Node* right = new Node(A[2]);

        root->left = left;
        root->right = right;
        
        for(int i = 3; i < N; i += 2) {
            Node* new_root = new Node(A[i]);
            Node* new_right = i == N-1 ? NULL : new Node(A[i + 1]);
            
            new_root->left = root;
            new_root->right = new_right;
    
            root = new_root;
        }

        return root;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148651357-db462745-6c59-4abf-a47c-e176cc324f58.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=3c5d82802df6e9e0e7ab4b6a9a4210cb&pid=700281&user=jhasuraj)
