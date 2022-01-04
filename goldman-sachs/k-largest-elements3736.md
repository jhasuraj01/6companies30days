# Max 10 numbers in a list having 10M entries (K largest elements)

[![Problem Link](https://img.shields.io/badge/GeeksforGeeks-298D46?style=for-the-badge&logo=geeksforgeeks&logoColor=white)](https://practice.geeksforgeeks.org/problems/k-largest-elements3736/1)

Given an array of N positive integers, print k largest elements from the array. 

### Sample Input
```
5 2
12 5 787 1 23
```
### Sample Output
```
787 23
```

### Solution
```cpp
class Solution
{
    public:
    vector<int> kLargest(int arr[], int n, int k)
    {
        priority_queue<int, vector<int>, greater<int> >pq;

        for(int i = 0; i < k; ++i) {
            pq.push(arr[i]);
        }

        for(int i = k; i < n; ++i) {
            if(pq.top() < arr[i]) {
                pq.pop();
                pq.push(arr[i]);
            }
        }

        vector<int> ans;
        while (!pq.empty()) {
            ans.push_back(pq.top());
            pq.pop();
        }

        reverse(ans.begin(), ans.end());

        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148006098-f8d17cd0-bdec-4dd0-bb60-ae04b9082c02.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=40ca7928d3a443a6779ea07f3e96a8ff&pid=701352&user=jhasuraj)
