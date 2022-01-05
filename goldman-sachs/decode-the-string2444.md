# Decode the string

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/decode-the-string2444/1#)

An encoded string (s) is given, the task is to decode it. The pattern in which the strings were encoded were as follows

**original string:** abbbababbbababbbab 

**encoded string:** 3[a3[b]1[ab]]

### Sample Input
```
3[b2[ca]]
```
### Sample Output
```
bcacabcacabcaca
```

### Solution
```cpp
class Solution{
public:
    string decodeRecursive(string &s, int left, int right) {

        int depth = 0, start, end, count = 1;
        string str = "", decoded = "";
        bool push = false, collecting_number = false;

        for(int i = left; i <= right; ++i) {
            char c = s[i];
            
            if(c == '[') {
                if(depth == 0) {
                    start = i+1;
                }
                ++depth;
            }
            else if(c == ']') {
                --depth;
                if(depth == 0) {
                    end = i-1;
                }
            }

            if(depth == 0) {

                if('0' <= c && c <= '9') {
                    while(!collecting_number && count--) decoded += str;
                    if(!collecting_number) count = 0;
                    str = "";
                    count = count * 10 + c - '0';
                    collecting_number = true;
                }
                else {
                    collecting_number = false;
                }

                if(c == ']') {
                    str += decodeRecursive(s, start, end);
                    while(!collecting_number && count--) decoded += str;
                    count = 1;
                    str = "";
                }
                else if('a' <= c && c <= 'z') {
                    str += c;
                }

            }
        }

        while(count--) decoded += str;

        return decoded;

    }
    string decodedString(string s){
        return decodeRecursive(s, 0, s.size() - 1);
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148205466-119ae2ee-06df-48e2-a1fa-801018534c71.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=461e6f8673561496a9b93480ef7abdb8&pid=705287&user=jhasuraj)
