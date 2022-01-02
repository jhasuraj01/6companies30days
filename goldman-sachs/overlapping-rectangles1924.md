# Overlapping Rectangles

[![Problem Link](https://img.shields.io/badge/GeeksforGeeks-298D46?style=for-the-badge&logo=geeksforgeeks&logoColor=white)](https://practice.geeksforgeeks.org/problems/overlapping-rectangles1924/1/)

Given two rectangles, find if the given two rectangles overlap or not. A rectangle is denoted by providing the x and y coordinates of two points: the left top corner and the right bottom corner of the rectangle. Two rectangles sharing a side are considered overlapping. (L1 and R1 are the extreme points of the first rectangle and L2 and R2 are the extreme points of the second rectangle).

**Note:** It may be assumed that the rectangles are parallel to the coordinate axis.
![image](https://user-images.githubusercontent.com/44930179/147873497-c32af86c-7ec6-414a-9b17-96cd24f0485d.png)

### Sample Input
```
0 10 10 0 5 5 15 0
```
### Sample Output
```
1
```

### Solution
```cpp
class Solution {
  public:
    int doOverlap(int L1[], int R1[], int L2[], int R2[]) {
        
        if(
            L2[0] - R1[0] > 0 ||
            R1[1] - L2[1] > 0 ||
            L1[0] - R2[0] > 0 ||
            R2[1] - L1[1] > 0
        ) {
            return 0;
        }
        else {
            return 1;
        }
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/147874937-e1581315-4bbf-43c6-b9f9-32819b9ac118.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=86b4ef19ca53a2d09b332f260a8acc8c&pid=705474&user=jhasuraj)

