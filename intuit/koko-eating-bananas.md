# Koko Eating Bananas

[![Problem Link](../assets/lc.svg)](https://leetcode.com/problems/koko-eating-bananas/)

Koko loves to eat bananas. There are n piles of bananas, the ith pile has piles[i] bananas. The guards have gone and will come back in h hours.

Koko can decide her bananas-per-hour eating speed of k. Each hour, she chooses some pile of bananas and eats k bananas from that pile. If the pile has less than k bananas, she eats all of them instead and will not eat any more bananas during this hour.

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

Return the minimum integer k such that she can eat all the bananas within h hours.

### Example 1
```
Input: piles = [3,6,7,11], h = 8
Output: 4
```

### Example 2
```
Input: piles = [30,11,23,4,20], h = 5
Output: 30
```

### Solution
```cpp
class Solution {
public:
    int minEatingSpeed(vector<int>& piles, int H) {
        int low = 1;
        int high = *max_element(piles.begin(), piles.end());
        int ans = high;

        while(low < high) {
            int mid = (low + high) >> 1;

            int h = 0;
            for(int bananas: piles) {
                h += ceil((double) bananas/mid);
            }
 
            if(h == H) {
                ans = min(ans, mid);
            }
            
            if(h > H) {
                low = mid + 1;
            }
            else {
                high = mid;
            }
        }

        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151487000-1706a427-fe23-47d9-8a88-45e133ef3ae0.png)](https://leetcode.com/submissions/detail/629360419/)