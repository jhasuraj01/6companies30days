# Generate Random Point in a Circle

[![Problem Link](../assets/lc.svg)](https://leetcode.com/problems/generate-random-point-in-a-circle/)

Given the radius and the position of the center of a circle, implement the function randPoint which generates a uniform random point inside the circle.

Implement the Solution class:

- `Solution(double radius, double x_center, double y_center)` initializes the object with the radius of the circle radius and the position of the center (x_center, y_center).
- `randPoint()` returns a random point inside the circle. A point on the circumference of the circle is considered to be in the circle. The answer is returned as an array [x, y].
 

### Example
```
Input
["Solution", "randPoint", "randPoint", "randPoint"]
[[1.0, 0.0, 0.0], [], [], []]
Output
[null, [-0.02493, -0.38077], [0.82314, 0.38945], [0.36572, 0.17248]]
```

### Solution
```cpp
class Solution {
public:
    double radius, x_center, y_center;
    Solution(double _radius, double _x_center, double _y_center) {
        radius = _radius;
        x_center = _x_center;
        y_center = _y_center;
    }
    
    vector<double> randPoint() {
        double theta = ((double) rand()/RAND_MAX)*2*M_PI;
        double r = sqrt((double) rand()/RAND_MAX) * radius;
        double x = r * cos(theta) + x_center;
        double y = r * sin(theta) + y_center;
        return {x, y};
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151700196-1851394e-bcba-4207-8224-eb8f61d3e5c0.png)](https://leetcode.com/submissions/detail/630910231/)
