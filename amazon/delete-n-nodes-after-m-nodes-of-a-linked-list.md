# Delete N nodes after M nodes of a linked list

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/delete-n-nodes-after-m-nodes-of-a-linked-list/1/#)

Given a linked list, delete N nodes after skipping M nodes of a linked list until the last of the linked list.

#### Input:

First line of input contains number of testcases T. For each testcase, first line of input contains number of elements in the linked list and next M and N respectively space separated. The last line contains the elements of the linked list.

#### Output:

Function should not print any output to stdin/console.

#### User Task:

The task is to complete the function linkdelete() which should modify the linked list as required.

### Sample Input
```
2
8
2 1
9 1 3 5 9 4 10 1 
6
1 2
8 4 8 10 1 3
```
### Sample Output
```
9 1 5 9 10 1 
8 10 
```

### Solution
```cpp
class Solution
{
    public:
    void linkdelete(struct Node  *head, int M, int N)
    {
        Node* node = head;

        while(node != NULL) {
            for(int i = 1; i < M && node != NULL; ++i) {
                node = node->next;
            }
            
            if(node == NULL) return;

            Node* ref = node;

            for(int i = 0; i <= N && node != NULL; ++i) {
                node = node->next;
            }

            ref->next = node;

        }
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148642312-8560bab6-27b6-407d-bc86-e86b5474a913.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=e43f1cb34ef47f0369f9454d37b9b699&pid=700021&user=jhasuraj)
