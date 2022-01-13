# Stickler Thief

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/stickler-theif-1587115621/1/#)

Stickler the thief wants to loot money from a society having n houses in a single line. He is a weird person and follows a certain rule when looting the houses. According to the rule, he will never loot two consecutive houses. At the same time, he wants to maximize the amount he loots. The thief knows which house has what amount of money but is unable to come up with an optimal looting strategy. He asks for your help to find the maximum money he can get if he strictly follows the rule. Each house has a[i]amount of money present in it.

### Sample Input
```
6
5 5 10 100 10 5
```

### Sample Output
```
110
```

### Solution
```cpp
class Solution {
    public:
    int FindMaxSum(int arr[], int n)
    {
        if(n == 1) return arr[0];
        if(n == 2) return max(arr[0], arr[1]);

        arr[2] = max(arr[1], arr[0] + arr[2]);

        for(int i = 3; i < n; ++i) {
            arr[i] = max({arr[i-1], arr[i-2] + arr[i], arr[i-3] + arr[i]});
        }

        return arr[n-1];
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149344488-97fa4032-232d-48d0-a860-bda01e0b7816.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=cd0d611d17ad820f079db007fe143235&pid=701417&user=jhasuraj)
