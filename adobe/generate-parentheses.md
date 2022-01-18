# Generate Parentheses

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/generate-all-possible-parentheses/1/#)

Given an integer N representing the number of pairs of parentheses, the task is to generate all combinations of well-formed(balanced) parentheses.

### Sample Input
```
3
```
### Sample Output
```
((()))
(()())
(())()
()(())
()()()
```

### Solution
```cpp
class Solution {
    public:
    void pattern(int n, int open, int close, string s, vector<string> &ans) {
        if(open == n && close == n) {
            return ans.push_back(s);
        }
        if(open < n) {
            pattern(n, open + 1, close, s + '(', ans);
        }
        if(open > close) {
            pattern(n, open, close + 1, s + ')', ans);
        }
    }

    vector<string> AllParenthesis(int n) {
        vector<string> ans;
        pattern(n, 0, 0, "", ans);
        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149923973-1777b359-6627-4b29-acd0-f7dd582c6037.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=a703d0e72585724ad446ae4d64033987&pid=702078&user=jhasuraj)
