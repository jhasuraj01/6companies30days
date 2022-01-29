# Maximum Height Tree

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/maximum-height-tree4803/1/#)

Given N dots that form a triangle such that ith line contains i number of dots.
```
    .
   . .
  . . .
 . . . .
```
Find the minimum hieght H of the triangle that can be formed using these N dots.

### Sample Input
```
10
```
### Sample Output
```
4
```

### Solution
```cpp
class Solution{
public:
    int height(int N){
        return (-1 + sqrt(1 + 8*N))/2;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151655051-4ce1e493-6d23-40a1-8632-1c6705fe474b.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=c36067d2317bac4ee2d37ff7e3919c68&pid=705111&user=jhasuraj)
