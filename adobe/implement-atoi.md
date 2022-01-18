# Implement Atoi

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/implement-atoi/1/#)

Your task  is to implement the function atoi. The function takes a string(str) as argument and converts it to an integer and returns it.

**Note:** You are not allowed to use inbuilt function.

### Sample Input
```
123
```

### Sample Output
```
123
```

### Solution
```cpp
class Solution {
  public:
    int atoi(string str) {
        int num = 0, fact = 1;
        if(str[0] == '-') {
            fact = -1;
            str = str.substr(1);
        }
        for(char c: str) {
            if(c - '0' < 0 || c - '0' > 9) {
                num = -1;
                fact = 1;
                break;
            }
            num = num * 10 + c - '0';
        }
        return num * fact;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149929396-d6c217a2-0047-4735-bcaa-f3faabafb162.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=5e574a145f8c02018e51925409f67075&pid=700386&user=jhasuraj)
