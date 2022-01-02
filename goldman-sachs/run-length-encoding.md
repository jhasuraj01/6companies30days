# Run Length Encoding

[![Problem Link](https://img.shields.io/badge/GeeksforGeeks-298D46?style=for-the-badge&logo=geeksforgeeks&logoColor=white)](https://practice.geeksforgeeks.org/problems/run-length-encoding/1/)

Given a string, Your task is to  complete the function `encode` that returns the run length encoded string for the given string.
eg if the input string is “wwwwaaadexxxxxx”, then the function should return “w4a3d1e1x6″.
You are required to complete the function `encode` that takes only one argument the string which is to be encoded and returns the encoded string.


### Sample Input
```
aaaabbbccc
```
### Sample Output
```
a4b3c3
```

### Solution
```cpp
string encode(string src)
{     
  char last = '-';
  string ans = "";
  int count = 0;

  for(char c: src) {
      if(c != last) {
          if(count) {
              ans += to_string(count);
          }
          ans += c;
          count = 1;
      }
      else {
          ++count;
      }
      last = c;
  }
  ans += to_string(count);
  
  return ans;
}
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/147875692-c421cfe9-70cc-4e28-9c40-d93cb6791bfa.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=40cf8cfde94db6354f0182a6793bcadf&pid=700243&user=jhasuraj)

