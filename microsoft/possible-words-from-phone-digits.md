# Possible Words From Phone Digits

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/possible-words-from-phone-digits-1587115620/1/#)

Given a keypad as shown in the diagram, and an N digit number which is represented by array `a[]`, the task is to list all words which are possible by pressing these numbers.

![image](https://user-images.githubusercontent.com/44930179/149143296-16eeecc9-79d2-40ac-b091-8206ecd5e5d1.png)

### Sample Input
```
3
2 3 4
```
### Sample Output
```
adg adh adi aeg aeh aei afg afh afi bdg bdh bdi beg beh bei bfg bfh bfi cdg cdh cdi ceg ceh cei cfg cfh cfi 
```

### Solution
```cpp
class Solution {
    public:
    vector<string> possibleWords(int a[], int N, int index = 0) {
        vector<vector<string>> keyboard = {
            {},
            {},
            {"a", "b", "c"},
            {"d", "e", "f"},
            {"g", "h", "i"},
            {"j", "k", "l"},
            {"m", "n", "o"},
            {"p", "q", "r", "s"},
            {"t", "u", "v"},
            {"w", "x", "y", "z"}
        };

        if(index == N - 1) {
            return keyboard[a[index]];
        }

        vector<string> ans;
        vector<string> postfixes = possibleWords(a, N, index + 1);

        for(string c: keyboard[a[index]]) {
            for(string s: postfixes) {
                ans.push_back(c + s);
            }
        }

        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149142873-fcb2977c-354b-472d-96a3-1712f979f2df.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=b5cded5bb9bd33598f54a8cd7fd835a5&pid=701199&user=jhasuraj)
