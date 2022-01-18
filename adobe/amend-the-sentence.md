# Amend The Sentence

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/amend-the-sentence3235/1#)

Given a string which is basically a sentence without spaces between words. However the first letter of every word is in uppercase. You need to print this sentence after following amendments:

1. Put a single space between these words
2. Convert the uppercase letters to lowercase.

**Note:** The first character of the string can be both uppercase/lowercase.


### Sample Input
```
BruceWayneIsBatman
```
### Sample Output
```
bruce wayne is batman
```

### Solution
```cpp
class Solution {
    public:
    string amendSentence (string s)
    {
        string ans = "";
        for(char c: s) {
            if(c >= 'A' && c <= 'Z') {
                if(ans.size()) {
                    ans += ' ';
                }
                ans += (c - 'A' + 'a');
            }
            else {
                ans += c;
            }
        }
        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149934293-9702b814-8e66-4f74-ae2c-3c0776a366b1.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=f3166f048edc0b6b73f01f3f14b81167&pid=702907&user=jhasuraj)
