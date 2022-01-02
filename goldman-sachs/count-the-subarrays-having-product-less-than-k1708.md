# Count the subarrays having product less than k

[![Problem Link](https://img.shields.io/badge/GeeksforGeeks-298D46?style=for-the-badge&logo=geeksforgeeks&logoColor=white)](https://practice.geeksforgeeks.org/problems/count-the-subarrays-having-product-less-than-k1708/1/)

Given an array of positive numbers, the task is to find the number of possible contiguous subarrays having product less than a given number k.

### Sample Input
```
4 10
1 2 3 4
```
### Sample Output
```
7
```

### Solution
```cpp
class Solution{
  public:
    int countSubArrayProductLessThanK(const vector<int>& a, int n, long long k) {
        int left = 0;
        int right = 0;
        long long prod = 1;
        int count = 0;

        for(int i = 0; i < n; ++i) {
            right = i;
            
            prod *= a[right];
            count += right - left + 1;
            
            while(prod >= k) {
                prod /= a[left++];
                count -= 1;
            }
        }
        
        return count;
    }
};
```

### Accepted

[![image](https://user-images.githubusercontent.com/44930179/147875288-7a331373-0f73-42be-948a-942a4ec355c8.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=5c7858d0d792b06c87077adf6e8d99d8&pid=703804&user=jhasuraj)
