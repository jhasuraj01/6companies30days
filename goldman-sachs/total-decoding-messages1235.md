# Total Decoding Messages

[![Problem Link](https://img.shields.io/badge/GeeksforGeeks-298D46?style=for-the-badge&logo=geeksforgeeks&logoColor=white)](https://practice.geeksforgeeks.org/problems/total-decoding-messages1235/1/#)

A top secret message containing letters from A-Z is being encoded to numbers using the following mapping:
```
'A' -> 1
'B' -> 2
 .
 .
'Z' -> 26
```
You are an FBI agent. You have to determine the total number of ways that message can be decoded, as the answer can be large return the answer modulo 109 + 7.

**Note:** An empty digit sequence is considered to have one decoding. It may be assumed that the input contains valid digits from 0 to 9 and If there are leading 0’s, extra trailing 0’s and two or more consecutive 0’s then it is an invalid string.

### Sample Input
```
123
```
### Sample Output
```
3
```

### Solution
```cpp
class Solution {
	public:
	    map<int, int> cache;
	    int mod = 1e9+7;
		int CountWays(string str, int n = 0){

		    if(str[0] == '0') return 0;

		    int end = str.size() - n - 1;

		    if(end < 1) return 1;

		    if(cache.count(end)) return cache[end];

		    int count = 0;
		    if(str[end] != '0') {
		        count = CountWays(str, n + 1);
		    }

		    if(str[end-1] == '1' || (str[end-1] == '2' && str[end] <= '6')) {
		        count += CountWays(str, n + 2);
		    }

		    cache[end] = count % mod;

		    return count % mod;
		}

};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148186941-d0f5fe4c-4c7c-45f2-964c-d41f76cd6acb.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=6849c8e3a93717352c31f0134df5a6dd&pid=705327&user=jhasuraj)
