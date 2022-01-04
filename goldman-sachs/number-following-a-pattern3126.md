# Number following a pattern

[![Problem Link](https://img.shields.io/badge/GeeksforGeeks-298D46?style=for-the-badge&logo=geeksforgeeks&logoColor=white)](https://practice.geeksforgeeks.org/problems/number-following-a-pattern3126/1#)

Given a pattern containing only I's and D's. I for increasing and D for decreasing.

Devise an algorithm to print the minimum number following that pattern.

Digits from 1-9 and digits can't repeat.

### Sample Input
```
D
```
### Sample Output
```
21
```

### Solution
```cpp
class Solution{   
public:
    string printMinNumberForPattern(string S){

        vector<int>num(S.size() + 1, 0);
        num[0] = 1;

        int max_int = 1;

        for(int i = 0; i < S.size(); ++i) {
            if(S[i] == 'I') {
                ++max_int;
                num[i + 1] = max_int;
            }

            int r = 0;
            while(i - r >= 0 && S[i - r] == 'D') {
                num[i - r + 1] = num[i - r];
                ++num[i - r];
                max_int = max(max_int, num[i - r]);
                ++r;
            }
        }

        for(auto n : num) {
            cout << n;
        }

        return "";
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148004212-1c7bab20-5683-41f2-a8e7-dce637706273.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=beb86d3e6d93f9ab3a81610235da44f9&pid=703607&user=jhasuraj)
