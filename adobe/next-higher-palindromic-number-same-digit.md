# Next higher palindromic number using the same set of digits

Given a palindromic number N in the form of string. The task is to find the smallest palindromic number greater than N using the same set of digits as in N.

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/next-higher-palindromic-number-using-the-same-set-of-digits5859/1/#)

### Sample Input
```
1
454121454
```

### Sample Output
```
514424415
```

### Solution
```cpp
class Solution {
  public:

    string nextPalin(string N) {
        int len = N.size();

        if(len <= 3) {
            return "-1";
        }

        int mid = len/2;

        int first_small = -1;

        for(int i = mid - 1; i > 0; --i) {
            if(N[i-1] < N[i]){
                first_small = i-1;
                break;
            }
        }
        
        if(first_small < 0) {
            return "-1";
        }

        int later_small = first_small + 1;
        for(int i = later_small; i < mid; ++i) {
            if(N[later_small] > N[i] && N[i] > N[first_small]) {
                later_small = i;
            }
        }

        swap(N[later_small], N[first_small]);
        swap(N[len - later_small - 1], N[len - first_small - 1]);

        sort(N.begin() + first_small + 1, N.begin() + mid);
        sort(N.rbegin() + first_small + 1, N.rbegin() + mid);

        return N;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/150862164-ecff246e-8c64-483d-913c-848d767fa66c.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=e6aeaec93727164cc195a1a0d58aa5d8&pid=703481&user=jhasuraj)