# Count Number of SubTrees having given Sum

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/count-number-of-subtrees-having-given-sum/1/#)


Given a binary tree and an integer ``x``. Your task is to complete the function ``countSubtreesWithSumX()`` that returns the count of the number of subtress having total node’s data sum equal to the value ``x``.

Example: For the tree given below:            
```
        5
     /    \
  -10      3
  / \     / \
 9   8  -4   7
```

Subtree with sum 7:
```
   -10
  /   \
 9     8
```
and one node 7.

### Sample Input
```
5 -10 3 9 8 -4 7
7
```
### Sample Output
```
2
```

### Solution
```cpp
pair<int, int> subtreeSum(Node* root, int x) {

    if(root == NULL) return {0, 0};

    int count = 0;

    pair<int, int> left = subtreeSum(root->left, x);
    pair<int, int> right = subtreeSum(root->right, x);

    count += left.first;
    count += right.first;

    int sum = left.second + right.second + root->data;

    if(sum == x) {
        ++count;
    }

    return {count, sum};
}

int countSubtreesWithSumX(Node* root, int x)
{
	pair<int, int> result = subtreeSum(root, x);
	return result.first;
}
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149342326-7775ba04-9b9b-4b3a-a9ad-cb0ea09143f9.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=51172c08317c0f21c30621a15a116b2d&pid=700689&user=jhasuraj)
