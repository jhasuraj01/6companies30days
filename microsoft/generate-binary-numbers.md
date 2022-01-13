# Generate Binary Numbers

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/generate-binary-numbers-1587115620/1/#)

Given a number N. The task is to generate and print all binary numbers with decimal values from 1 to N.

### Sample Input
```
2
```
### Sample Output
```
1
10
```

### Solution
```cpp
vector<string> generate(int N) {
    vector<string> ans(N);

	for(int i = 1; i <= N; ++i) {
	    int num = i;
	    while(num) {
	        ans[i - 1] += (char) ('0' + (num & 1));
	        num >>= 1;
	    }
	    reverse(ans[i - 1].begin(), ans[i - 1].end());
	}

	return ans;
}
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149350805-bad92a4c-0a71-484a-a615-be810001d68d.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=e42367210e9eabd08f63daa13922d5a5&pid=701347&user=jhasuraj)
