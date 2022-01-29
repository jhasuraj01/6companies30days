# Find the Kth Largest Integer in the Array

[![Problem Link](../assets/lc.svg)](https://leetcode.com/problems/find-the-kth-largest-integer-in-the-array/)

You are given an array of strings nums and an integer k. Each string in nums represents an integer without leading zeros.

Return the string that represents the kth largest integer in nums.

**Note:** Duplicate numbers should be counted distinctly. For example, if nums is ["1","2","2"], "2" is the first largest integer, "2" is the second-largest integer, and "1" is the third-largest integer.

### Example 1
```
Input: nums = ["3","6","7","10"], k = 4
Output: "3"
```

### Example 2
```
Input: nums = ["2","21","12","1"], k = 3
Output: "2"
```

### Solution
```cpp
class Solution {
public:
    string kthLargestNumber(vector<string>& nums, int k) {
        sort(nums.begin(), nums.end(), [&](string a, string b) {
            if(a.size() != b.size()) {
                return a.size() < b.size();
            }
            else {
                return a < b;
            }
        });
        for(auto n: nums) cout << n << " ";
        return nums.end()[-k];
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151655578-04f9517e-6c25-49f6-90a3-dbeddfa42f18.png)](https://leetcode.com/submissions/detail/630107466/)
