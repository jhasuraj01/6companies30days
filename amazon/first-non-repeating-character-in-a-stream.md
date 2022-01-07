# First non-repeating character in a stream

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/first-non-repeating-character-in-a-stream1216/1#)

Given an input stream of A of n characters consisting only of lower case alphabets. The task is to find the first non repeating character, each time a character is inserted to the stream. If there is no such character then append '#' to the answer.

### Sample Input
```
zzabbc
```
### Sample Output
```
z#aaaa
```

### Solution
```cpp
class Solution {
	public:
    string FirstNonRepeating(string A){

        // non repeating characters queue
        queue<char> nrcq;
        vector<int> used(26, false);

        string ans = "";

        for(int i = 0; i < A.size(); ++i) {
            char c = A[i];
            char output;
            
            if(used[c - 'a'] < 1) {
                nrcq.push(c);
            }
            ++used[c - 'a'];

            while(!nrcq.empty() && used[nrcq.front() - 'a'] > 1) {
                nrcq.pop();
            }

            if(nrcq.empty()) {
                output = '#';
            }
            else {
                output = nrcq.front();
            }
            ans += output;
        }
        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148503297-3554906f-127e-4425-9c6f-65693ab4a84f.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=34c5bef29fc8c889ba9433ae7d76cb4f&pid=705333&user=jhasuraj)
