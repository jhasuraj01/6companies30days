# Minimum steps to destination

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/minimum-number-of-steps-to-reach-a-given-number5234/1/#)

Given an infinite number line. You start at 0 and can go either to the left or to the right. The condition is that in the ith move, youmust take i steps. Given a destination D , find the minimum number of steps required to reach that destination.

### Sample Input
```
5
```
### Sample Output
```
5
```

### Naive Solution
```cpp
class Solution {
public:
    int minSteps(int D, int position = 0, int lastStep = 0) {
        
        if(abs(position) == D) return 0;
        else if(abs(position) > D) return numeric_limits<int>::max();

        return min(
            minSteps(D, position + lastStep + 1, lastStep + 1),
            minSteps(D, position - lastStep - 1, lastStep + 1)
        ) + 1;
        
    }
};
```

### Solution
```cpp
class Solution {
public:
    int minSteps(int D) {
        
        int steps = ((double)-1 + sqrt(1 + 8*D)) / (double) 2;
        int coverage = (steps * (steps + 1))/2;

        if(coverage == D) return steps;

        for(int i = 0; i < 3; ++i) {
            ++steps;
            coverage += steps;
            if(((coverage - D) & 1) == 0) {
                return steps;
            }
        }
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149411999-d9b5c713-5a71-4bd8-8d68-ffbe1ecbc692.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=3f7014dcbd2ec679dc5d04de3334f3d1&pid=704560&user=jhasuraj)
