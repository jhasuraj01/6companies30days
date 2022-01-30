# Remove Colored Pieces if Both Neighbors are the Same Color

[![Problem Link](../assets/lc.svg)](link)

### Example 1
```
Input: colors = "AAABABB"
Output: true
```

### Example 2
```
Input: colors = "AA"
Output: false
```

### Solution
```cpp
class Solution {
public:
    
    bool winnerOfGame(string colors) {
        
        vector<int> A, B;
    
        char last_color = '-';

        for(char c: colors) {
            if(last_color == c) {
                if(c == 'A') ++A.back();
                else ++B.back();
            }
            else {
                if(c == 'A') A.push_back(1);
                else B.push_back(1);
            }
            last_color = c;
        }

        int alice = 0,  bob = 0;

        for(int &a: A) alice += max(0, a - 2);

        for(int &b: B) bob += max(0, b - 2);

        return alice > bob;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151698158-c3d8339c-de8f-443b-b956-2287494310b6.png)](https://leetcode.com/submissions/detail/630887028/)
