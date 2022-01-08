# Nuts and Bolts Problem

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/nuts-and-bolts-problem0431/1#)

Given a set of N nuts of different sizes and N bolts of different sizes. There is a one-one mapping between nuts and bolts. Match nuts and bolts efficiently.

Comparison of a nut to another nut or a bolt to another bolt is not allowed. It means nut can only be compared with bolt and bolt can only be compared with nut to see which one is bigger/smaller.

The elements should follow the following order ! # $ % & * @ ^ ~ .

### Sample Input
```
5
@ % $ # ^
% @ # $ ^
```
### Sample Output
```
# $ % @ ^ 
# $ % @ ^ 
```

### Solution
```cpp
class Solution{
public:	

	void matchPairs(char nuts[], char bolts[], int n) {

        // align nuts and bolts
	    for(int i = 0; i < n; ++i) {
	        for(int j = i; j < n; ++j) {
	            if(bolts[j] == nuts[i]) {
	                char temp = bolts[i];
	                bolts[i] = bolts[j];
	                bolts[j] = temp;
	                continue;
	            }
	        }
	    }
	    
        // find original position in an array
	    vector<int> order(n);
        iota(order.begin(), order.end(), 0);
        sort(order.begin(), order.end(), [&](int i, int j) {
            return nuts[i] < bolts[j];
        });
        
        // place nuts and bolts on its original position
        for(int i = 0; i < n; ++i) {
            nuts[i] = bolts[order[i]];
        }
        for(int j = 0; j < n; ++j) {
            bolts[j] = nuts[j];
        }

	}
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148646462-a1272bd9-3fef-47b4-b24d-0dedac962f3d.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=c65327e32ba6ef9d9f3c9741244ef0b3&pid=703024&user=jhasuraj)
