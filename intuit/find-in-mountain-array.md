# Find in Mountain Array

[![Problem Link](../assets/lc.svg)](https://leetcode.com/problems/find-in-mountain-array/)

Given a mountain array mountainArr, return the minimum index such that mountainArr.get(index) == target. If such an index does not exist, return -1.

### Example 1
```
Input: array = [1,2,3,4,5,3,1], target = 3
Output: 2
```

### Example 2
```
Input: array = [0,1,2,4,2,1], target = 3
Output: -1
```

### Solution
```cpp
/**
 * // This is the MountainArray's API interface.
 * // You should not implement it, or speculate about its implementation
 * class MountainArray {
 *   public:
 *     int get(int index);
 *     int length();
 * };
 */

class Solution {
public:
    int binarySearch(int target, MountainArray &mountainArr, int left, int right, bool asc) {
        while(left <= right) {
            int mid = (left + right)/2;
            
            int val = mountainArr.get(mid);

            if(val == target) {
                return mid;
            }
            if(asc) {
                if(val > target) {
                    right = mid - 1;
                }
                else {
                    left = mid + 1;
                }
            }
            else {
                if(val > target) {
                    left = mid + 1;
                }
                else {
                    right = mid - 1;
                }
            }
        }
        return -1;
    }
    int findInMountainArray(int target, MountainArray &mountainArr) {
        int length = mountainArr.length();
        
        int left = 0, right = length - 1, mid, peek;
        
        while(left < right) {
            mid = (left + right)/2;
            
            int a = mountainArr.get(mid);
            int b = mountainArr.get(mid + 1);
            
            if(a > b) {
                right = mid;
                peek = mid;
            }
            else {
                left = mid + 1;
                peek = mid + 1;
            }
        }
        
        int leftSearch = binarySearch(target, mountainArr, 0, peek, true);
        if(leftSearch >= 0) return leftSearch;

        int rightSearch = binarySearch(target, mountainArr, peek, length - 1, false);
        return rightSearch;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151037066-1483903c-ac65-465a-b6e1-afe38d4b0bf1.png)](https://leetcode.com/submissions/detail/627700749/)
