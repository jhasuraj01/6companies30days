# Ugly Numbers

[![Problem Link](https://img.shields.io/badge/GeeksforGeeks-298D46?style=for-the-badge&logo=geeksforgeeks&logoColor=white)](https://practice.geeksforgeeks.org/problems/ugly-numbers2254/1/)

Ugly numbers are numbers whose only prime factors are 2, 3 or 5. The sequence 1, 2, 3, 4, 5, 6, 8, 9, 10, 12, 15, … shows the first 11 ugly numbers. By convention, 1 is included. Write a program to find Nth Ugly Number.

### Sample Input
```
10
```
### Sample Output
```
12
```

### Solution
```cpp
class Solution{
public:	
	// #define ull unsigned long long
	/* Function to get the nth ugly number*/
	ull getNthUglyNo(int n) {
	    vector<long long> ugly_nums(n + 1);
	    ugly_nums[1] = 1;
	    int p2 = 1, p3 = 1, p5 = 1;

	    for(int i = 2; i <= n; ++i) {
	        ugly_nums[i] = min({ 2ll * ugly_nums[p2], 3ll * ugly_nums[p3], 5ll * ugly_nums[p5] });
	        if(ugly_nums[i] == 2ll * ugly_nums[p2]) ++p2;
	        if(ugly_nums[i] == 3ll * ugly_nums[p3]) ++p3;
	        if(ugly_nums[i] == 5ll * ugly_nums[p5]) ++p5;
	    }

	    return ugly_nums.back();
	}
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/147880234-8b1011f7-0c60-405d-be48-457d3e533ade.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=2eb0648341e23e7fd4f1cfeb64421cde&pid=703093&user=jhasuraj)
