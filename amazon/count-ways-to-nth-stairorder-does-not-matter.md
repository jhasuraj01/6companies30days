# Count ways to N'th Stair(Order does not matter)

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/count-ways-to-nth-stairorder-does-not-matter1322/1/#)

There are N stairs, and a person standing at the bottom wants to reach the top. The person can climb either 1 stair or 2 stairs at a time. Count the number of ways, the person can reach the top (order does not matter).

**Note:** Order does not matter means for n=4 {1 2 1},{2 1 1},{1 1 2} are considered same.

### Hint
```
n = 2i + j;

4 = 2(0) + 4
4 = 2(1) + 2
4 = 2(2) + 0
```

### Sample Input
```
4
```
### Sample Output
```
3
```

### Solution
```cpp
class Solution
{
    public:
    long long countWays(int m)
    {
        return m/2 + 1ll;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148505727-7510508d-f574-40d3-83cd-96c58655d936.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=8304d762c9435b549cbc78bd4048142e&pid=701419&user=jhasuraj)
