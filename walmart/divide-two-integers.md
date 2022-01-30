# Divide Two Integers

[![Problem Link](../assets/lc.svg)](https://leetcode.com/problems/divide-two-integers/)

Given two integers dividend and divisor, divide two integers without using multiplication, division, and mod operator.

The integer division should truncate toward zero, which means losing its fractional part. For example, 8.345 would be truncated to 8, and -2.7335 would be truncated to -2.

Return the quotient after dividing dividend by divisor.

**Note:** Assume we are dealing with an environment that could only store integers within the 32-bit signed integer range: [−231, 231 − 1]. For this problem, if the quotient is strictly greater than 231 - 1, then return 231 - 1, and if the quotient is strictly less than -231, then return -231.

### Example 1
```
Input: dividend = 10, divisor = 3
Output: 3
```

### Example 2
```
Input: dividend = 7, divisor = -3
Output: -2
```

### Solution
```cpp
class Solution {
public:
    int divide(long long dividend, long long divisor) {
        
        bool difSign = (dividend > 0ll) ^ (divisor > 0ll);

        dividend = labs(dividend);
        divisor = labs(divisor);

        long long quotient = 0;

        while(dividend > 0ll) {
            int count = 0;

            while((dividend - (divisor << (count + 1))) >= 0) count++;

            dividend -= divisor << count;

            if(dividend >= 0ll) {
                quotient += (1ll << count);
            }
        }

        return min((difSign ? -quotient : quotient), (long long) 2147483647);
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151701468-c76c4fca-68ff-4f37-a48b-ab951aaeb097.png)](https://leetcode.com/submissions/detail/630924752/)