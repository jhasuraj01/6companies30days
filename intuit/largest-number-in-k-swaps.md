# Largest number in K swaps

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/largest-number-in-k-swaps-1587115620/1#)

Given a number K and string str of digits denoting a positive integer, build the largest number possible by performing swap operations on the digits of str at most K times.

### Sample Input
```
1
3
6278134320804246
```

### Sample Output
```
8876634320204241
```

### Solution
```cpp
class Solution {
    public:
    void swap(char &a, char &b) {
        a = a ^ b;
        b = a ^ b;
        a = a ^ b;
    }

    string findMaximumNum(string &str, int k, int index = 0)
    {
       int length = str.length();

       if(k == 0 || index >= length) {
           return str;
       }

       int max_index = index;
       vector<int> max_indices;

        for(int i = index + 1; i < length; ++i) {
            if(str[max_index] <= str[i]) {
                if(str[max_index] < str[i]) {
                    max_indices.clear();
                }
                max_index = i;
                max_indices.push_back(i);
            }
        }

        if(str[max_index] == str[index]) {
            return findMaximumNum(str, k, index + 1);
        }

        string ans = str;

        for(int max_index: max_indices) {
            swap(str[max_index], str[index]);
            ans = max(ans, findMaximumNum(str, k - 1, index + 1));
            swap(str[max_index], str[index]);
        }

        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/150641755-8a91bbb8-67dd-4a2a-94b6-505157a658b8.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=a2ac5f73bc57db27668984a121f07139&pid=701369&user=jhasuraj)