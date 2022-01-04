# Find Missing And Repeating

[![Problem Link](https://img.shields.io/badge/GeeksforGeeks-298D46?style=for-the-badge&logo=geeksforgeeks&logoColor=white)](https://practice.geeksforgeeks.org/problems/find-missing-and-repeating2512/1/#)

Given an unsorted array Arr of size N of positive integers. One number 'A' from set {1, 2, …N} is missing and one number 'B' occurs twice in array. Find these two numbers.

### Sample Input
```
2
2 2
```
### Sample Output
```
2 1
```

### Solution
> Time: O(N), Space: O(N)
```cpp
class Solution{
public:
    int *findTwoElement(int *arr, int n) {
        vector<bool> nums(n+1, 0);

        int repeated;
        
        int ans[2];

        for(int i = 0; i < n; ++i) {
            int num = arr[i];
            if(nums[num]) {
                ans[0] = num;
            }
            nums[num] = nums[num] ^ 1;
        }

        for(int i = 1; i <= n; ++i) {
            if(nums[i] == 0 && i != ans[0]) {
                ans[1] = i;
                break;
            }
        }

        int *ptr;
        ptr = ans;

        return ptr;

    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148010626-6fae09b8-a44a-4c11-8f39-ae1f2a6183ef.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=5fc89ed14fb72d9cf92175879d66431b&pid=702678&user=jhasuraj)
