# Column name from a given column number

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/column-name-from-a-given-column-number4244/1/#)

Given a positive integer, return its corresponding column title as appear in an Excel sheet.

Excel columns has a pattern like A, B, C, … ,Z, AA, AB, AC,…. ,AZ, BA, BB, … ZZ, AAA, AAB ….. etc. In other words, column 1 is named as “A”, column 2 as “B”, column 27 as “AA” and so on.

### Sample Input
```
28
```
### Sample Output
```
AB
```

### Solution
```cpp
class Solution{
    public:
    string colName (long long int n)
    {
        string ans;

        while(n) {
            ans += (char) ('A' + (n-1) % 26);
            n = (n-1)/26;
        }
        
        reverse(ans.begin(), ans.end());
        
        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148641450-73de6bfd-1508-4daf-83c6-f2c042f0a35a.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=b6b1fdf3d26d74a8be26883c95f7443a&pid=702959&user=jhasuraj)
